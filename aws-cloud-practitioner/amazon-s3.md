# Amazon S3

**Amazon Simple Storage Service (S3)** is a highly scalable, durable, and secure object storage service provided by AWS. It is designed to store and retrieve any amount of data from anywhere on the web.

<!-- TOC depthFrom:2 -->
- [Overview](#overview)
- [Buckets](#s3---buckets)
- [Objects](#s3---objects) 
<!-- /TOC -->

#### Key Features:
- **Scalability**: Automatically scales to handle vast amounts of data.
- **Durability**: Offers 99.999999999% (11 nines) durability by redundantly storing data across multiple Availability Zones.
- **Security**: Provides comprehensive security and compliance capabilities, including data encryption at rest and in transit, and fine-grained access controls using AWS Identity and Access Management (IAM).
- **Data Management**: Features lifecycle policies for automatic data migration to different storage classes, versioning, and object tagging.
- **Performance**: Delivers high-performance access to data with low latency and high throughput.
- **Storage Classes**: Offers multiple storage classes tailored to different use cases, such as:
  - **S3 Standard**: For frequently accessed data.
  - **S3 Intelligent-Tiering**: Automatically moves data between two access tiers (frequent and infrequent) when access patterns change.
  - **S3 Standard-IA (Infrequent Access)**: For data accessed less frequently, but requires rapid access when needed.
  - **S3 Glacier**: For long-term archival with retrieval times ranging from minutes to hours.
  - **S3 Glacier Deep Archive**: For data that is rarely accessed and can be retrieved within 12 hours.

#### Use Cases:
- **Backup and Restore**: Reliable storage for backup and disaster recovery solutions.
- **Big Data Analytics**: Scalable storage for data lakes and analytics applications.
- **Content Storage and Distribution**: Efficiently stores and delivers static content, including media files and documents.
- **Archiving**: Long-term archival of important data with cost-effective storage options.

Amazon S3's flexibility, scalability, and robust feature set make it an essential service for a wide range of cloud storage needs, from simple file storage to complex data management and analytics solutions.


## S3 - Buckets

* **Object Storage**: `Amazon S3` allows storing objects (files) in containers called _Buckets_ (similar to directories).
* **Unique Naming**: Buckets must have a globally unique name across all AWS accounts and regions.
* **Region-Level Definition**: Buckets are defined and created within a specific AWS region.
* **Naming Conventions**:
  * No uppercase letters or underscores.
  * Length must be between 3-63 characters.
  * Cannot be formatted as an IP address.
  * Must start with a lowercase letter or a number.
  * Must **not** start with the prefix `xn--`.
  * Must **not** end with the suffix `-s3alias`.


## S3 - Objects

* **Objects**: Files stored in `S3` are referred to as objects, each with a unique key.
* **Key**: The full path to the object.
  * Example: `s3://the_bucket/the_file.txt`
  * Example: `s3://the_bucket/the_folder/another_folder/the_file.txt`
* **Key Composition**: The key consists of a `prefix` and an `object name`.
  * Example: `s3://the_bucket/prefix{the_folder/another_folder/}object_name{the_file.txt}`
* **Directory Concept**: `S3` does not have actual directories; instead, it uses keys with slashes to simulate folder structures.
* **Object Values**: The content or body of the object.
  * Maximum object size is 5TB (5000GB).
  * Objects larger than 5GB must be uploaded using the `multi-part upload` feature.
* **Metadata**: A list of text key/value pairs that can be system-defined or user-defined.
* **Tags**: Unicode key/value pairs (up to 10) used for organizing, managing, and controlling access to objects.
* **Version ID**: Unique identifier for each version of an object (if versioning is enabled).




