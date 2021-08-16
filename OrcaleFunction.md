<u>**Oracle Function as a service**</u>

- Oracle Functions is a fully managed, multi-tenant, highly scalable, on-demand, Functions-as-a-Service platform. 
- It is built on enterprise-grade Oracle Cloud Infrastructure and powered by the Fn Project open source engine. 
- Use Oracle Functions (sometimes abbreviated to just Functions) when you want to focus on writing code to meet business needs.

- **Oracle Functions is based on Fn Project**. Fn Project is an open source, container native, serverless platform that can be run anywhere - any cloud or on-premises. 
- Fn Project is easy to use, extensi730be, and performant. You can download and install the open source distribution of Fn Project, develop and test a function locally, and then use the same tooling to deploy that function to Oracle Functions.
- Oracle Functions is integrated with Oracle Cloud Infrastructure Identity and Access Management (IAM), which provides easy authentication with native Oracle Cloud Infrastructure identity functionality. 
- 

Invoking function:

- You can create automation based on state changes for your Oracle Cloud Infrastructure resources by using event types, rules, and actions. 

- We can have events in other services invoke functions in Oracle Functions such as:
  The Events service
  The Notifications service
  The API Gateway service
  The Oracle Integration service
  The Service Connector Hub service
  The Streaming service



- Each service in Oracle Cloud Infrastructure integrates with IAM for authentication and authorization, for all interfaces

**Oracle Functions Capabilities and Limits**:

- Like any other Oracle cloud resource, the number of functions and applications you can create in a region is controlled by Oracle Functions service limits (the default limit based upon your payment plan, and you can increase by submitting a request).

- The maximum amount of data you can send to a function (the function's request payload) and the maximum amount of data a function can return in response to a request (the function's response payload) is 6MB. Both these limits are fixed and can't be changed.


The following Oracle Functions resources emit events:

applications
functions

What are Applications ?

- Application is logical grouping of functions, where we define common context to store configuration variables that are available to all functions in the application, it is like container, where we specify the subnets, we specify whether to enable logging for the function etc.

- When functions from different applications are invoked simultaneously, Oracle Functions ensures these function executions are isolated from each other.

- Best practice is to group multiple functions in a single application for better efficiency and performance.

- Oracle Functions shows applications and their functions in the Console.

What is Function?

- A function is a piece of code, stored in an application. Functions are stored as Docker images in a specified Docker registry. A function can be invoked in response to a CLI comand ot signed HTTP requests.

- A definition of the function is stored as metadata in the Oracle Functions server. The definition describes how the function is to be executed and includes:
  the Docker image to pull when the function is invoked
  the maximum length of time the function is allowed to execute for
  the maximum amount of memory the function is allowed to consume



Invocations

- In Oracle Functions, a function's code is run (or executed) when the function is called (or invoked). You can invoke a function that you've deployed to Oracle Functions from:

The Fn Project CLI.
The Oracle Cloud Infrastructure SDKs.
Signed HTTP requests to the function's invoke endpoint. Every function has an invoke endpoint.
Other Oracle Cloud services (for example, triggered by an event in the Events service) or from external services.


When a function is invoked for the first time, Oracle Functions pulls the function's Docker image from the specified Docker registry, runs it as a Docker container, and executes the function. If there are subsequent requests to the same function, Oracle Functions directs those requests to the same container. After a period being idle, the Docker container is removed.

Triggers
A trigger is the result of an action elsewhere in the system, that sends a request to invoke a function in Oracle Functions. A function might not be associated with any triggers, or it can be associated with one or multiple triggers.



What Happens When You Deploy a Function to Oracle Functions?

When you have written the code for a function and it's ready to deploy, you can use a single Fn Project CLI command to perform all the deploy operations in sequence:

building a Docker image from the function
providing a definition of the function in a func.yaml file that includes:
the maximum length of time the function is allowed to execute for
the maximum amount of memory the function is allowed to consume
pushing the image to the specified Docker registry
uploading function metadata (including the memory and time restrictions, and a link to the image in the Docker registry) to the Fn Server
adding the function to the list of functions shown in the Console


What Happens When You Invoke a Function?

You can invoke a function that you've deployed to Oracle Functions from:

The Fn Project CLI.
The Oracle Cloud Infrastructure SDKs.
Signed HTTP requests to the function's invoke endpoint. Every function has an invoke endpoint.
Other Oracle Cloud services (for example, triggered by an event in the Events service) or from external services.
When a function is invoked f

When a function is invoked for the first time, Oracle Functions first verifies the request with the IAM service. Assuming the request passes authentication and authorization checks, Oracle Functions then passes the request to the Fn Server, which uses the function definition to:


identify the Docker image of the function to pull from the Docker registry
execute the function by running the function's image as a container on an instance in a subnet associated with the application to which the function belongs


When the function is executing inside the container, the function can read from and write to other resources and services running in the same subnet (for example, Database as a Service). 

The function can also read from and write to other shared resources (for example, Object Storage), and other Oracle Cloud Services. You can specify the maximum length of time the function is allowed to execute by setting a timeout in the func.yaml file or in the Console.


Oracle Functions stores the function's logs in Oracle Cloud Infrastructure or in an external logging destination.


When the function has finished executing and after a period being idle, the Docker container is removed.

If Oracle Functions receives another call to the same function before the container is removed, the second request is routed to the same running container

If Oracle Functions receives a call to a function that is currently executing inside a running container, Oracle Functions scales horizontally to serve both incoming requests and a second Docker container is started.





Resiliency and Availability
In the case of Oracle Functions:

The control plane is a set of components that manages function definitions.
The data plane is a set of components that executes functions in response to invocation requests.


For resiliency and high availability, both the control plane and data plane components are distributed across different availability domains and fault domains in a region.

If one of the domains ceases to be available, the components in the remaining domains take over to ensure that function definition management and execution are not disrupted.

Concurrency and Scalability

In the case of Functions, when a function is invoked for the first time, the function's image is run as a container on an instance in a subnet associated with the application to which the function belongs. When the function is executing inside the container, the function can read from and write to other shared resources and services running in the same subnet (for example, Database as a Service). The function can also read from and write to other shared resources (for example, Object Storage), and other Oracle Cloud Services.

If Oracle Functions receives multiple calls to a function that is currently executing inside a running container, Oracle Functions automatically and seamlessly scales horizontally to serve all the incoming requests

Oracle Functions starts multiple Docker containers, up to the limit specified for your tenancy. The default limit is 60 GB of RAM reserved for function execution per availability domain, although you can request an increase to this limit

When functions from different applications are invoked simultaneously, Oracle Functions ensures these function executions are isolated from each other.

![image-20210808154235150](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808154235150.png)



![image-20210808154213125](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808154213125.png)



![image-20210808154354179](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808154354179.png)

![image-20210808154810830](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808154810830.png)





![image-20210808154933282](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808154933282.png)

![image-20210808160150071](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808160150071.png)

![image-20210808160209472](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808160209472.png)

![image-20210808160329132](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808160329132.png)

![image-20210808160428130](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808160428130.png)



![image-20210808160623531](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808160623531.png)

![image-20210808160946873](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808160946873.png)

![image-20210808164256284](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808164256284.png)

![image-20210808164316179](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808164316179.png)

![image-20210808164405375](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808164405375.png)





![image-20210808164437021](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808164437021.png)



![image-20210808164606904](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808164606904.png)



![image-20210808164630729](C:\Users\rahchaub\AppData\Roaming\Typora\typora-user-images\image-20210808164630729.png)





