**<u>VPN connection between OCI and Azure</u>**





![img](https://cdn-images-1.medium.com/max/1200/1*YPm6MKP4oSAZw88DetL05Q.png)







In this talk we are going to discuss:

- how to connect your Oracle Cloud Infrastructure virtual cloud network (VCN) with  AWS cloud.
- We are going to use Site-to-Site VPN with a Libreswan VM as the customer-premises equipment (CPE).
- Resources in the OCI and AWS will able to communicate with each other using their private IP addresses as if they are in the same network segment.

**What is Liberswan** **?**

- Libreswan is a *free software* implementation of the most widely supported and standardized VPN protocol using **"IPsec"** and the *Internet Key Exchange* (**"IKE"**). 
- These standards are produced and maintained by the *Internet Engineering Task Force* (**"IETF"**).
- Libreswan supports both route-based and policy-based tunnels.

**<u>Steps:</u>**

#1 : Install Liberswan : We will install Liberswan on host in AWS.
#2: Architecture Diagram:

![img](https://docs.oracle.com/en-us/iaas/Content/Resources/Images/network_libreswan_architecture.png)





Step #1: **<u>Follow the follows steps at AWS side</u>**

1.1: Login to EC2 instance
![img](https://cdn-images-1.medium.com/max/1200/1*-kVFt58CtANsl-CCkrv7PQ.png)



1.2 Install the Libeswan package: yum -y install liberswan

![img](https://cdn-images-1.medium.com/max/1200/1*dd-P3nhqW7-HsbxsMycMgA.png)


1.3: In the AWS Console, disable the source and destination checks on the Libreswan VM instance by right-clicking the instance, clicking Networking, and then clicking Change Source/Dest. Check. When prompted, click Yes, Disable
![img](https://cdn-images-1.medium.com/max/1200/1*Ytm91kpeg3AmvOl7IMSskg.png)


![img](https://cdn-images-1.medium.com/max/1200/1*EbYoYryEruuer3O74ghsXw.png)



Why we are making this change?

Each EC2 instance performs source/destination checks by default. This means that the instance must be the source or destination of any traffic it sends or receives. However, in our case this **instance must be able to send and receive traffic when the source or destination is not itself**. Therefore, we have to disable source/destination checks for this instance.



![img](https://cdn-images-1.medium.com/max/1200/1*iMX4eml_az7dn_B-BnZGsg.png)



In the AWS Console, edit your AWS route table. Add a rule with the VCN CIDR (172.0.0.0/16) as the destination and the AWS Libreswan instance ID (  i-0cb60d0e228882453  in this example) as the target.

**What is Route Table?**

- A route table contains rules about how IP packets can travel to different IP addresses out of the VPC(AWS)/VCN(OCI). 
- Each rule specifies destination CIDR block and it specifies the route target, the next hop for the traffic that matches that CIDR.
- A route table is used only if the destination IP address is not within the VPC's CIDR block. (Local rule).
-  However this local rule is not there in OCI VCNs, that has been automatically taken care. In OCI, you don't require any route rules in order to enable traffic within the VCN itself.
- 

![img](https://cdn-images-1.medium.com/max/1200/1*st8-n_TphKZ0lvZHqHAH7A.png)

So, here you can see that there is an entry which says 172.0.0.0/16, is my destination CIDR, packets destined to this CIDR address, they need to go to instance i-0cb60d0e228882453 (which is now acting as a gateway).





In the AWS Console, enable inbound TCP and UDP traffic on ports 4500 and 500 to allow an Oracle Cloud Infrastructure Site-to-Site VPN IPSec connection with the AWS Libreswan VM. 

![img](https://cdn-images-1.medium.com/max/1200/1*FgU-YWzCiofVsTpXHc_pmg.png)











![image-20210802162541167](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210802162541167.png)



![image-20210802162703601](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210802162703601.png)

![image-20210802162919130](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210802162919130.png)



net.ipv4.ip_forward=1
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.all.send_redirects = 0
net.ipv4.conf.default.send_redirects = 0
net.ipv4.conf.eth0.send_redirects = 0
net.ipv4.conf.default.accept_redirects = 0
net.ipv4.conf.eth0.accept_redirects = 0



![image-20210802163024021](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210802163024021.png)





![image-20210802171247053](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210802171247053.png)



![image-20210802171637369](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210802171637369.png)



![image-20210802171654930](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210802171654930.png)



950-967-4897