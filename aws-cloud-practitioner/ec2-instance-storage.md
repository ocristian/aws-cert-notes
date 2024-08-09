# EC2 - Instance Storage

`EC2 Instance Storage` provides temporary, high-performance storage directly attached to an instance.  
This storage is ideal for temporary data that changes frequently, such as buffers, caches, and scratch data. It is ephemeral, meaning the data is lost when the instance is stopped or terminated.  
For persistent storage, use [Amazon EBS](#ebs-volume) or `Amazon S3`.

<!-- TOC depthFrom:2 -->
- [Summary](#summary)
- [EBS Volume](#ebs-volume)
- [AWS AMI - Amazon Machine Image](#aws-ami---amazon-machine-image)
- [AWS EC2 Image Builder](#aws-ec2-image-builder)
- [AWS EC2 Instance Store](#aws-ec2-instance-store)
- [AWS EFS - Elastic File System](#aws-efs---elastic-file-system)
- [AWS EFS IA - Infrequent Access](#aws-efs-ia---infrequent-access) 
- [AWS EBS vs EFS](#aws-ebs-vs-efs)
- [AWS FSx Overview](#aws-fsx-overview) 
- [EC2 Storage - Shared Responsibility Model](#ec2-storage---shared-responsibility-model)
<!-- /TOC -->

## EC2 - Instance Storage


<a name="summary"></a>
### Summary

* **EBS Volumes**:
  * **Network Drives**: Attached to one EC2 instance at a time.
  * **Availability Zone (AZ)**: Mapped to a specific AZ.
  * **Snapshots**: Use EBS snapshots for backups and transferring EBS volumes across AZs.
  * **AMI (Amazon Machine Image)**: Create ready-to-use EC2 instances with custom configurations.
  * **EC2 Image Builder**: Automatically build, test, and distribute AMIs.

* **EC2 Instance Store**:
  * **High Performance**: High-performance hardware disk attached to an EC2 instance.
  * **Ephemeral Storage**: Data is lost if the instance is stopped or terminated.

* **EFS (Elastic File System)**:
  * **Network File System**: Can be attached to multiple instances within a region.
  * **EFS Infrequent Access (EFS-IA)**: Cost-optimized storage class for infrequently accessed files.

* **Amazon FSx**:
  * **FSx for Windows File Server**: Managed network file system for Windows workloads.
  * **FSx for Lustre**: High-performance file system for compute-intensive Linux applications.


<a name="ebs-volume"></a>
### EBS Volume

`EBS - Elastic Block Store` is a high-performance, scalable block storage service,  designed for use with `Amazon EC2` instances.  

**Key features include:**
- **Persistence**: Data is retained even after the `EC2` instance is stopped or terminated.
- **Types**: Offers various volume types, including General Purpose SSD (gp3, gp2), Provisioned IOPS SSD (io2, io1), Throughput Optimized HDD (st1), and Cold HDD (sc1), catering to different performance needs and cost considerations.
- **Scalability**: Volumes can be dynamically resized to accommodate growing data.
- **Durability**: Provides redundancy within an Availability Zone (AZ) to protect against hardware failures.
- **Snapshots**: Allows taking point-in-time snapshots, which can be used for backups, data migration, or creating new volumes.
- **Encryption**: Supports encryption at rest and in transit for data security.
- **Delete on Termination Attribute**: Controls the behavior of EBS volumes when an EC2 instance terminates.
  - By default, the root EBS volume is deleted when Delete on Termination is enabled.
  - By default, any other attached EBS volumes are not deleted when Delete on Termination is disabled.

EBS volumes are ideal for applications requiring consistent and low-latency performance, such as databases, file systems, and enterprise applications.

#### Summary

* **Network Drive**:
    * Uses network communication with the instance, introducing minor latency.
    * Can be detached from one EC2 instance and attached to another quickly.

* **Availability Zone (AZ) Specific**:
    * Locked to a specific AZ, e.g., an EBS volume in `us-east-1a` cannot be attached to `us-east-1b`.
    * To move a volume across AZs, you need to create a snapshot and restore it in the desired AZ.

* **Provisioned Capacity**:
    * Configured with a specific size (in GBs) and IOPS (Input/Output Operations Per Second).
    * Billing is based on the provisioned capacity, regardless of usage.
    * Capacity can be increased over time without downtime.


## AWS AMI - Amazon Machine Image

AMI - An `Amazon Machine Image` is a template that contains the software configuration (OS, application server, and applications) required to launch an EC2 instance.  

**Key aspects include:**

- **Pre-configured**: Includes an operating system, software packages, and application servers.
- **Customizable**: Users can create their own AMIs by customizing existing instances and saving the configuration.
- **Reusability**: Enables rapid scaling by launching multiple instances with the same configuration.
- **Sharing**: AMIs can be shared with other AWS accounts or kept private.
- **Region Specific**: AMIs are built for a specific region but can be copied across regions.
- **Launching**: EC2 instances can be launched from:
  - **Public AMI**: Provided by AWS.
  - **Your Own AMI**: Custom-built and maintained by you.
  - **AWS Marketplace AMI**: Created by third parties, potentially requiring payment.

AMIs are essential for creating consistent, reproducible instances in cloud environments.


### AMI Process (from an EC2 Instance)

- **Start an EC2 instance and customize it**
  - Launch a new EC2 instance and install the necessary software, applications, and configurations.

- **Stop the instance for data integrity**
  - Stop the EC2 instance to ensure that the data is in a consistent state before creating the AMI.

- **Build an AMI, which will also create the EBS snapshot**
  - Create an AMI from the stopped instance. This process will capture the configuration of the instance and create a snapshot of the associated EBS volumes.

- **Launch instances from the AMI**
  - Use the created AMI to launch new instances with the same configuration and data.


<a name="ec2-image-builder"></a>
## AWS EC2 Image Builder

`AWS EC2 Image Builder` is a fully managed service that simplifies the creation, maintenance, and deployment of customized and secure Amazon Machine Images (AMIs). 
It automates the image creation process, ensuring that your images are up-to-date and compliant with your security and application requirements.

### Key Features:

- **Automated Image Creation**: Define a pipeline to automatically build and test images based on a schedule or triggered by updates.
- **Customization**: Include software, configurations, and settings tailored to your needs.
- **Security**: Integrate security updates and compliance checks into the image creation process.
- **Version Control**: Manage versions of your images, making it easy to roll back to previous versions if necessary.
- **Integration**: Easily integrates with other AWS services like EC2, Amazon S3, and AWS Systems Manager.

### Use Cases:

- **Consistent Environments**: Ensure consistent and repeatable environments for development, testing, and production.
- **Security Compliance**: Automate the inclusion of security patches and updates.
- **Application Deployment**: Simplify the deployment of applications with pre-configured environments.

By using `EC2 Image Builder`, you can streamline the process of creating and managing your AMIs, reducing manual effort and enhancing security and compliance.


## AWS EC2 Instance Store

`AWS EC2 Instance Store` provides temporary block-level storage for your EC2 instances. 
This storage is physically attached to the host machine and offers high I/O performance. It is ideal for applications that require temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content.

### Key Features:

- **High Performance**: Provides low-latency, high-throughput storage directly attached to the instance.
- **Ephemeral Storage**: Data in instance store is temporary and is lost if the instance is stopped, terminated, or fails.
- **Cost-Effective**: No additional cost as it is included in the cost of the instance.

### Use Cases:

- **Temporary Data**: Ideal for temporary storage needs such as cache or scratch space.
- **High I/O Applications**: Suitable for applications requiring high I/O performance, like big data processing and large-scale simulations.

### Limitations:

- **Data Persistence**: Data is not persistent and will be lost upon instance termination, stop, or failure.
- **Backup Requirements**: Critical data should be backed up to persistent storage like Amazon EBS or Amazon S3.

By leveraging `EC2 Instance Store`, you can achieve high-performance storage for ephemeral data needs, ensuring optimal application performance without incurring additional costs.


## AWS EFS - Elastic File System

`AWS Elastic File System (EFS)` is a fully managed, scalable, and elastic NFS (Network File System) file system for use with AWS Cloud services and on-premises resources. 
It allows you to create and configure file systems that are automatically and instantly scalable, enabling multiple EC2 instances to access and share data concurrently with high performance.

### Key Features:

- **Scalability**: Automatically scales your file system storage up or down based on your application needs, with no provisioning required.
- **High Availability and Durability**: Data is stored across multiple Availability Zones (AZs) in an AWS region, providing redundancy and high availability.
- **Performance Modes**: Offers General Purpose and Max I/O performance modes to optimize for latency-sensitive and throughput-intensive workloads.
- **Access Controls**: Integrates with AWS IAM and provides POSIX-compliant file system permissions, allowing fine-grained access control.

### Use Cases:

- **Content Management**: Ideal for content repositories, media workflows, and large-scale data processing.
- **Web Serving**: Suitable for web serving environments where multiple web servers need shared access to the same files.
- **Big Data and Analytics**: Facilitates data analysis by providing shared access to data across multiple compute instances.

### Integration:

- **EC2 and Lambda**: Seamlessly integrates with Amazon EC2 instances and AWS Lambda, providing persistent file storage.
- **On-Premises Access**: Can be accessed from on-premises environments using AWS Direct Connect or VPN.

AWS EFS simplifies the process of managing file storage, providing a scalable and resilient solution for a wide range of applications and workloads.


## AWS EFS IA - Infrequent Access

`AWS EFS Infrequent Access (EFS IA)` is a storage class within `Amazon Elastic File System (EFS)` designed for storing files that are not accessed frequently. 
This storage class offers a lower-cost option for data that does not require constant access, while still providing the benefits of EFS such as scalability and availability.

### Key Features:

- **Cost-Effective**: Offers a lower price per gigabyte compared to the standard EFS storage class, making it cost-efficient for data that is rarely accessed.
- **Automatic Lifecycle Management**: Automatically moves files between the standard storage class and the Infrequent Access storage class based on access patterns, ensuring optimal storage costs.
- **High Availability and Durability**: Like the standard EFS storage class, EFS IA provides high availability and durability by storing data redundantly across multiple Availability Zones (AZs).
- **Performance**: Suitable for files that are accessed less frequently but still require the same performance when accessed.

### Use Cases:

- **Archival Storage**: Ideal for storing files that are rarely accessed but must be retained for compliance or regulatory reasons.
- **Backup and Recovery**: Suitable for backup files and recovery snapshots that do not require frequent access.
- **Historical Data**: Perfect for data that needs to be preserved over the long term but is not actively used.

### Benefits:

- **Cost Savings**: Significant cost reductions for storing infrequently accessed data, reducing overall storage costs.
- **Seamless Access**: Files in the EFS IA storage class are automatically accessible without any changes to applications, maintaining the same ease of use as standard EFS.

EFS Infrequent Access helps optimize storage costs while ensuring that data remains available and durable, making it a valuable option for managing large datasets with varying access patterns.


## AWS EBS vs EFS

AWS provides two distinct storage options: `Amazon Elastic Block Store (EBS)` and `Amazon Elastic File System (EFS)`. 
While both are designed to store data and integrate with EC2 instances, they serve different use cases and have distinct characteristics.

### Amazon Elastic Block Store (EBS)

- **Type of Storage**: Block storage.
- **Use Case**: Ideal for use as the primary storage for a single instance.
- **Performance**: High-performance storage for databases, file systems, and applications requiring low-latency access.
- **Persistence**: Data persists independently of the instance; volumes can be attached, detached, and reattached to instances.
- **Scalability**: Must be manually scaled by provisioning additional or larger volumes.
- **Availability**: Data is stored in a single Availability Zone (AZ); snapshots can be taken for backup to Amazon S3.
- **Cost**: Pay for the provisioned capacity, regardless of how much is used.

### Amazon Elastic File System (EFS)

- **Type of Storage**: Network file system.
- **Use Case**: Suitable for use cases where multiple instances need to access the same data concurrently.
- **Performance**: Optimized for scalability and shared access, with performance modes for latency-sensitive and throughput-intensive workloads.
- **Persistence**: Data is stored across multiple Availability Zones (AZs) for redundancy and high availability.
- **Scalability**: Automatically scales up and down based on the amount of data stored.
- **Availability**: Highly available and durable, as data is distributed across multiple AZs.
- **Cost**: Pay for the amount of data stored, with options for Infrequent Access (IA) to reduce costs for data not accessed frequently.

### Summary:

- **EBS** is ideal for single-instance use cases requiring high-performance block storage and low-latency access, such as databases and applications.
- **EFS** is designed for scenarios where multiple instances need concurrent access to shared files, providing scalable and highly available file storage.

By understanding the key differences, you can choose the appropriate storage solution that best fits your workload requirements.


## AWS FSx Overview

`Amazon FSx` is a fully managed service that provides highly performant and scalable file systems on AWS. 
It offers multiple file system options designed for different use cases and performance requirements, allowing customers to easily lift and shift their applications without rewriting code.

### Key Features:

- **Multiple File Systems**:
  - **Amazon FSx for Windows File Server**: Provides fully managed, highly reliable, and scalable Windows file storage. It supports the SMB protocol, Windows NTFS, and Active Directory integration.
  - **Amazon FSx for Lustre**: Offers a high-performance file system optimized for fast processing of workloads such as big data and machine learning. It integrates with Amazon S3, providing fast access to S3 data.
  - **Amazon FSx for NetApp ONTAP**: Delivers a fully managed NetApp ONTAP file system, ideal for enterprise workloads that require advanced data management features.
  - **Amazon FSx for OpenZFS**: Provides a fully managed, scalable, and high-performance file storage service with OpenZFS, suitable for various enterprise applications.

- **Performance**:
  - **High Throughput and IOPS**: Designed to deliver high levels of throughput and IOPS, supporting demanding applications and workloads.
  - **Low Latency**: Ensures low-latency access to data, crucial for performance-sensitive applications.

- **Scalability**:
  - **Automatic Scaling**: Automatically scales storage and throughput to meet changing demands, eliminating the need for manual intervention.

- **Integration**:
  - **AWS Services**: Integrates seamlessly with other AWS services such as EC2, S3, and IAM.
  - **On-Premises**: Can be accessed from on-premises environments using AWS Direct Connect or VPN.

- **Security**:
  - **Encryption**: Supports encryption of data at rest and in transit to ensure data security.
  - **Access Controls**: Provides fine-grained access controls using AWS IAM and integrates with Active Directory for user authentication and authorization.

- **Ease of Use**:
  - **Managed Service**: Fully managed by AWS, reducing the operational overhead of managing file servers and storage.
  - **Compatibility**: Compatible with existing applications, enabling easy migration without code changes.

### Use Cases:

- **Enterprise Applications**: Suitable for enterprise workloads such as shared file storage, backup, and disaster recovery.
- **Big Data and Analytics**: Ideal for high-performance computing (HPC), data processing, and machine learning applications.
- **Content Management**: Supports content repositories, media processing, and web serving environments.

By providing multiple file system options tailored to different performance and feature requirements, Amazon FSx enables businesses to run a wide variety of applications efficiently and securely in the cloud.


<a name="ec2-storage-responsibility-model"></a>
## EC2 Storage - Shared Responsibility Model

### AWS Responsibilities
- **Infrastructure**: Managing the global security network and replication of data for EBS volumes and EFS drives.
- **Host Isolation**: Ensuring isolation on physical hosts to maintain security and performance.
- **Hardware Maintenance**: Replacing faulty hardware to ensure reliability and uptime.
- **Compliance**: Performing compliance validation to meet regulatory requirements.

### Your Responsibilities
- **Backup and Snapshot Procedures**: Setting up and managing backup and snapshot procedures to ensure data integrity and recovery.
- **Data Encryption**: Implementing data encryption both at rest and in transit to protect sensitive information.
- **Data Management**: Being responsible for any data stored on EBS volumes, EFS drives, and EC2 instance store.
- **Risk Understanding**: Understanding the risks associated with using EC2 Instance Store, which is ephemeral and not suitable for persistent storage.

By clearly delineating these responsibilities, AWS and users can ensure the security, reliability, and compliance of their EC2 storage environments.
