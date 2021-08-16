



**File Storage**

Oracle File Storage provides a fully managed Network File System (NFS) that scales automatically to accommodate growth up to 8 exabytes, eliminating the need to provision capacity in advance. Multiway replication ensures data availability and durability.

It was launched by Oracle cloud in Jan 2018. It is fully managed and highly managed service. It's a AD specific service.. It support NFS version 3 along with NLM with full POSIX semantics. You can use NFS client on windows to support File storage. By default you can create 100 File system per AD, and every file system scales automatically to accommodate the growth of up to 8 exabytes.

however this is a soft limit, you can always increase this by creating a support case with Oracle.

Mount Target in file storage is an NFS endpoint that lives in your subnet of choice. Mount targets are highly available, that you can use in mount command to access the file system. 

**Features**

- Snapshot and clone capabilities
- **Automatic elasticity** without provisioning
- Scalable from kilobytes to 8 exabytes
- Highly available, durable filesystems
- **Encryption** at **rest** by default using AES 256
- **Encryption** in **transit** supported by TLS 1.2
- Support for managing your own encryption keys
-  Pricing is based on the size of the File storage



**File Storage use cases**

- **Concurrent read and write operations**: File Storage ensures consistent file systems for concurrent read and write operations by multiple clients.

- **Higher availability and durability**: File Storage provides higher availability and durability for customers who need a fully managed service to handle a single point of failure.

- **Parallel workloads**: File Storage performs best with parallelized workloads and when running bulk operations.

- **Scale out access and capacity**: File Storage is best suited for applications that require scale-out access and capacity.
- **General Purpose File Storage** Access to an unlimited pool of file systems to manage growth of structured and unstructured data.
- **Big Data and Analytics:** Run analytic workloads and use shared file systems to store persistent data.
- **Lift and Shift of Enterprise Applications:** Migrate existing Oracle applications that need NFS storage, such as Oracle E-Business Suite and PeopleSoft.
- **Databases and Transactional Applications:** Run test and development workloads with Oracle, MySQL, or other databases.
- **Backups, Business Continuity, and Disaster Recovery:** Host a secondary copy of relevant file systems from on premises to the cloud for backup and disaster recovery purposes.
- **MicroServices and Docker:** Deliver stateful persistence for containers. Easily scale as your container-based environments grow.

**Concept**

**MOUNT TARGET**

- It is nothing but the NFS endpoints (IP address or DNS name), lives in a subnet of your choice. 
- In order to connect the NFS file system you have to use Mount Target in your command.
- File systems are exported through the mount targets.
- With a single mount target, we can make several file systems available on the network (by creating export in the mount target).
-  One thing to note here is that, one mount target can accept up to 100K NFS client connections.
- By default, you can create 2 mount target per account per availability Domain.
- It's a good idea to have a subnet created for the mount target in order to avoid the IP conflict.

![img](https://cdn-images-1.medium.com/max/1200/1*opDt-KfrYgIeI85mK18qKw.png)





**EXPORT**

- Exports control how NFS clients access file systems when they connect to a mount target.
- You can create as many exports in a mount target for a **single** file system as you wish.
- You can create as many exports in a mount target for **different** file systems as you wish.
- You can delete and re-create exports in a mount target as often as you need to.



**EXPORT SET**

- Collection of one or more exports that control what file systems the mount target exports using NFSv3 protocol and how those file systems are found using the NFS mount protocol.
- Each mount target has an export set.
- Each file system associated with the mount target has at least one export in the export set.



**EXPORT PATH**

- A path that is specified when an export is created.
- A file system is made available using export path using mount target (two file system associated with same Mount target can't have overlapping export path.)
- /abc and /abc/project are not allowed.
- It uniquely identifies the file system within the mount target, letting you associate many file systems to a single mount target.

![img](https://cdn-images-1.medium.com/max/1200/1*r8-FywIPLYay0gPEUhzZ7A.png)



**EXPORT OPTIONS**

-  Set of parameters within the export that specify the level of access granted to NFS clients when they connect to a mount target.



