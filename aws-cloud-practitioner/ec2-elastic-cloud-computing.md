# EC2 - Elastic Cloud Computing

`EC2` is a `AWS Global Service` where users, groups, roles and policies are created.

<!-- TOC depthFrom:2 -->
- [AWS Budget Setup](#aws-budget-setup)
- [Amazon EC2](#ec2-elastic-compute-cloud)
- [Sizing and Configuration Options](#ec2-sizing-and-configuration-options)
- [EC2 User Data](#ec2-user-data)
- [Instance Types](#ec2-instance-types)
- [Security Groups](#ec2-security-groups)
- [SSH](#ssh)
- [EC2 Instance Connect](#ec2-instance-connect)
- [EC2 IAM Roles](#ec2-iam-roles)
- [Instance Purchasing Options](#ec2-instance-purchasing-options)
- [Shared Responsibility Model](#ec2-shared-responsibility-model)
<!-- /TOC -->

<a name="aws-budget-setup"></a>
## AWS Budget Setup
Set custom budgets that alert you when you exceed your budgeted thresholds.

#### Best Practices
- **Granularity**: Use granular budgets for different projects, teams, or services.
- **Regular Review**: Regularly review and adjust budgets to align with business goals and usage patterns.
- **Forecasting**: Utilize forecasting features to predict future costs and adjust budgets accordingly.
- **Integration**: Integrate AWS Budgets with AWS Cost Explorer for more detailed cost analysis and insights.

## Amazon EC2

<a name="ec2-elastic-compute-cloud"></a>
### EC2 - Elastic Compute Cloud (Infrastructure as a Service)

It mainly consists of:
* Renting Virtual Machines (`EC2`)
* Storing data on virtual drives (`EBS`)
* Distributing Load across machines (`ELB`)
* Scaling services using auto-scaling group (`ASG`)

<a name="ec2-sizing-and-configuration-options"></a>

### EC2 - Sizing and Configuration Options

* **OS**: Linux, Windows or MacOS
* **CPU**: How much compute power and cores
* **RAM**: How much random-access memory
* **Storage**
  * **Network-attached**: `EBS` and `EFS`
  * **Hardware**: `EC2 Instance Store`
* **Network card**: Speed, Public IP address
* **Firewall Rules**: `Security Group`
* **Bootstrap Script**: `EC2 User Data` 


<a name="ec2-user-data"></a>
### EC2 User Data

To bootstrap instances using an `EC2 User Data` script, which executes commands when a machine starts, follow these guidelines:

- **Initialization**: The script runs only once, during the instance's first start.
- **Automated Boot Tasks**: Use the script to automate tasks such as:
    - Installing updates
    - Installing software
    - Downloading common files from the internet
    - Any other automation tasks required
- **Execution Privileges**: The `EC2 User Data` scripts run with root user privileges.

<a name="ec2-instance-types"></a>
### EC2 Instance Types

These examples highlight the variety of EC2 instance types for different workload needs.

**General Purpose**:
  - **t3.micro**: 2 vCPUs, 1 GiB memory. Ideal for low-traffic web servers and small databases.
  - **m6i.large**: 2 vCPUs, 8 GiB memory. Suitable for web applications and small databases.

**Compute Optimized**:
  - **c6i.xlarge**: 4 vCPUs, 8 GiB memory. Great for compute-bound applications like batch processing.

**Memory Optimized**:
  - **r6i.2xlarge**: 8 vCPUs, 64 GiB memory. Perfect for high-performance databases and big data analytics.
  - **x2iedn.4xlarge**: 16 vCPUs, 512 GiB memory. Ideal for large in-memory databases.

**Storage Optimized**:
  - **i4i.large**: 2 vCPUs, 16 GiB memory, 468 GB NVMe SSD. Suitable for high IOPS storage like NoSQL databases.
  - **d3.2xlarge**: 8 vCPUs, 64 GiB memory, 24 TB HDD. Designed for big data workloads.

**Accelerated Computing**:
  - **p4d.24xlarge**: 96 vCPUs, 1.1 TiB memory, 8 NVIDIA A100 GPUs. Optimized for machine learning and HPC.
  - **g5.2xlarge**: 8 vCPUs, 32 GiB memory, 1 NVIDIA A10G GPU. Suitable for 3D rendering and gaming.

More at [AWS EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/)

<a name="ec2-security-groups"></a>
### EC2 Security Groups

`EC2 Security Groups` are essential for network security in AWS, managing inbound and outbound traffic for EC2 instances.

- **Core Component**: Essential for network security in AWS.
- **Traffic Control**: Manage the inbound and outbound traffic for EC2 instances.
- **Rule Type**: Only contain **allow rules**; no deny rules are supported.
- **Rule References**: Rules can reference either specific **IP addresses** or other **security groups**.

#### Good to Know
- **Attach to Multiple Instances**: Security Groups can be associated with multiple EC2 instances simultaneously.
- **Region/VPC Bound**: They are specific to a Region and VPC combination.
- **Traffic Control**: Security Groups operate independently of EC2 instances. If traffic is blocked, the instance won’t receive it.
- **SSH Access**: It’s advisable to create a separate Security Group specifically for SSH access.
- **Troubleshooting**: If an application is inaccessible (e.g., timeout errors), it might be due to Security Group rules. Connection refused errors could indicate application issues or that the application isn’t running.
- **Default Rules**: By default, all inbound traffic is blocked, while all outbound traffic is allowed.

#### Ports to Know
- **22 (SSH)**: Secure Shell for logging into Linux instances.
- **21 (FTP)**: File Transfer Protocol for uploading files to a file share.
- **22 (SFTP)**: Secure File Transfer Protocol for secure file transfers over SSH.
- **80 (HTTP)**: Hypertext Transfer Protocol for accessing unsecured websites.
- **443 (HTTPS)**: Hypertext Transfer Protocol Secure for accessing secure websites.
- **3389 (RDP)**: Remote Desktop Protocol for logging into Windows instances.

<a name="ssh"></a>
### SSH Summary

`SSH` is a command-line tool used to securely control remote machines from `MacOS` or `Linux` systems.  
Here’s how to access a remote machine:

- **Basic Access**:
  ```shell
  ssh ec2-user@{public-ip-of-remote-instance}
  ```

- **Secure Access with Private Key**:
  ```shell
  ssh -i {private-key-file} ec2-user@{public-ip-of-remote-instance}
  ```
  Using a private key enhances security by providing encrypted authentication.

Replace `{public-ip-of-remote-instance}` with the actual public IP address of the remote instance and `{private-key-file}` with the path to your private key file.

<a name="ec2-instance-connect"></a>
### EC2 Instance Connect

`EC2 Instance Connect` is a secure and easy way to connect to your EC2 instances using SSH.  
It integrates with `AWS IAM` to provide temporary, time-limited SSH keys for authentication, eliminating the need to manage and distribute long-term SSH keys.  
You can connect via the `AWS Management Console`, `CLI`, or `API`, simplifying access management and enhancing security.

<a name="ec2-iam-roles"></a>
### EC2 IAM Roles

`EC2 IAM Roles` allow you to securely provide permissions to your EC2 instances to access other AWS services.  
Instead of embedding long-term access keys in your applications, you can assign an `IAM Role` to your instance, which provides temporary security credentials. This enhances security by managing permissions through IAM policies, enabling fine-grained access control and easier credential management.

<a name="ec2-instance-purchasing-options"></a>
### EC2 - Instance Purchasing Options

- **On-Demand Instances**: Ideal for short workloads with predictable pricing. Pay by the second.
- **Reserved Instances (1 and 3 years)**:
  - **Standard Reserved Instances**: For long-term workloads, offering significant savings.
  - **Convertible Reserved Instances**: For long-term workloads with the flexibility to change instance types.
- **Savings Plans (1 and 3 years)**: Commitment to a specific usage amount, providing savings for long-term workloads.
- **Spot Instances**: Suitable for short-term, cost-sensitive workloads. Offers low prices but instances can be terminated at any time.
- **Dedicated Hosts**: Rent an entire physical server, providing control over instance placement and allowing use of existing server-bound software licenses.
- **Dedicated Instances**: Ensures that no other customers share your hardware.
- **Capacity Reservations**: Reserve capacity in a specific Availability Zone for any duration, ensuring availability when needed. 


#### EC2 - On-Demand

- **Pay for What You Use**:
  - **Linux or Windows**: Billed per second, after the first minute.
  - **All Other Operating Systems**: Billed per hour.
- **Cost**: Highest cost, but no upfront payment.
- **Commitment**: No long-term commitment.
- **Recommended For**: **Short-term** and **uninterrupted workloads**, especially when the application's behavior is unpredictable.  


#### EC2 - Reserved Instances

- **Cost Savings**: Up to 72% discount compared to On-Demand instances.
- **Reservation Details**: Reserve specific instance attributes such as Instance Type, Region, Tenancy, and OS.
- **Reservation Period**: Choose between 1-year (lower discount) or 3-year (higher discount) terms.
- **Payment Options**:
  - **No Upfront**: Lower discount.
  - **Partial Upfront**: Medium discount.
  - **All Upfront**: Highest discount.
- **Scope**: Can be regional or zonal (reserve capacity in a specific Availability Zone).
- **Recommended For**: Steady-state usage applications, such as databases.
- **Marketplace**: Buy and sell Reserved Instances on the Reserved Instance Marketplace.

- **Convertible Reserved Instances**:
  - Flexibility to change instance type, family, OS, scope, and tenancy.
  - Up to 66% discount.

*Note: The discount percentages are illustrative examples.*


#### EC2 - Savings Plans

- **Discounts**: Save up to 72%, similar to Reserved Instances.
- **Commitment**: Commit to a specific usage amount (e.g., $10/hour) for 1 or 3 years.
- **Beyond Plan Usage**: Any usage beyond the Savings Plan commitment is billed at the On-Demand price.
- **Scope**: Typically locked to a specific instance family and AWS region (e.g., `M5` in `us-east-1`).
- **Flexibility**:
  - **Instance Size**: Apply savings to different sizes within the same family (e.g., m5.xlarge, m5.2xlarge).
  - **Operating System**: Applicable to various OS options (e.g., Linux, Windows).
  - **Tenancy**: Applies to different tenancy models (e.g., Host, Dedicated, Default).


#### EC2 - Spot Instances

- **Discounts**: Save up to 90% compared to On-Demand instances.
- **Interruption Risk**: Instances can be terminated if your maximum price is less than the current Spot price.
- **Cost Efficiency**: The most cost-efficient option in AWS.
- **Use Cases**: Ideal for workloads that can tolerate interruptions, such as:
  - Batch jobs
  - Data analysis
  - Image processing
  - Distributed workloads
  - Workloads with flexible start and end times
- **Limitations**: Not suitable for critical jobs or databases due to potential interruptions.


#### EC2 - Dedicated Hosts

- **Dedicated Server**: A physical server with EC2 instance capacity exclusively for your use.
- **Compliance and Licensing**: Ideal for addressing compliance requirements and using existing server-bound software licenses (per-socket, per-core, per-VM).
- **Purchasing Options**:
  - **On-Demand**: Pay per second for an active Dedicated Host.
  - **Reserved**: Commit to 1 or 3 years with No Upfront, Partial Upfront, or All Upfront payment options.
- **Cost**: The most expensive EC2 option.
- **Use Cases**:
  - Software with complex licensing models.
  - Companies with strong compliance or regulatory requirements.


#### EC2 - Dedicated Instances

- **Dedicated Hardware**: Instances run on hardware dedicated to your use.
- **Shared Hardware**: May share the hardware with other instances within the same account.
- **Instance Placement**: No control over instance placement; instances may move to different hardware after stop/start.

**Note**: Dedicated Instances provide your own instances on dedicated hardware, whereas Dedicated Hosts give you access to the entire physical server, offering greater visibility and control over lower-level hardware details.


#### EC2 - Capacity Reservation

- **Guaranteed Capacity**: Reserve On-Demand instance capacity in a specific Availability Zone (AZ) for any duration.
- **Reliable Access**: Ensure EC2 capacity is available when you need it.
- **Flexibility**: No time commitment; create or cancel at any time, but no billing discounts are provided.
- **Cost Management**: Combine with Regional Reserved Instances and Savings Plans to benefit from billing discounts.
- **On-Demand Billing**: Charged at On-Demand rates, whether instances are running or not.
- **Use Cases**: Ideal for short-term, uninterrupted workloads that must reside in a specific AZ.


<a name="ec2-shared-responsibility-model"></a>
### EC2 - Shared Responsibility Model

#### AWS Responsibilities
- **Infrastructure**: Managing the global security network.
- **Host Isolation**: Ensuring isolation on physical hosts.
- **Hardware Maintenance**: Replacing faulty hardware.
- **Compliance**: Performing compliance validation.

#### Your Responsibilities
- **Security Group Rules**: Configuring and managing Security Group rules.
- **OS Maintenance**: Applying patches and updates to the operating system.
- **Software Management**: Installing and maintaining software and utilities on the EC2 instance.
- **IAM Management**: Assigning IAM roles to EC2 instances and managing IAM user access.
- **Data Security**: Ensuring the security of data on your instance.  
