# Amazon S3

**Amazon Simple Storage Service (S3)** is a highly scalable, durable, and secure object storage service provided by AWS. It is designed to store and retrieve any amount of data from anywhere on the web.

<!-- TOC depthFrom:2 -->
- [Buckets](#s3---buckets)
- [Objects](#s3---objects) 
- [S3 - Security](#s3--security)
- [S3 - Policies](#s3--policies)
- [S3 - Static Website Hosting](#s3--static-website-hosting)
- [S3 - Versioning](#s3--versioning)
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


## S3 – Security

**Amazon S3** offers robust security features to protect data at both the object and bucket levels.  

### Key security mechanisms:

- **Access Control**: Utilize **AWS Identity and Access Management** (IAM) policies, bucket policies, and **Access Control Lists** (ACLs) to define and enforce granular permissions on who can access S3 resources.
- **Data Encryption**: Supports encryption for data at rest (using server-side encryption with AWS-managed keys, customer-managed keys, or customer-provided keys) and in transit (using SSL/TLS).
- **Block Public Access**: Provides the option to block public access to buckets and objects globally or at the bucket level, ensuring no unintended exposure.
- **S3 Object Lock**: Enables data immutability by preventing objects from being deleted or overwritten for a defined period or indefinitely, meeting compliance needs.
- **Logging and Monitoring**: Offers detailed logging through S3 Access Logs and AWS CloudTrail, allowing visibility into requests made to S3 for security audits.

These features make `Amazon S3` a secure solution for storing sensitive and critical data.


## S3 – Policies

**Amazon S3 Policies** control access to buckets and objects, allowing you to define who can interact with your `S3` resources and what actions they are permitted to perform.  

### There are two primary types of policies:

- **Bucket Policies**: JSON-based policies attached directly to an `S3` bucket. These policies define permissions for the entire bucket and its objects. You can specify who has access (users, roles, accounts), what actions they can take (e.g., `s3:GetObject`, `s3:PutObject`), and under what conditions access is granted (e.g., source IP address, SSL requirement).
- **IAM Policies**: Permissions assigned to specific AWS users, groups, or roles through `IAM`. These policies define what actions a particular `IAM` entity can perform on `S3` resources, regardless of bucket policy.

### Policy Structure

Policies are written in `JSON` and consist of:
- **Actions**: Operations allowed or denied (e.g., `s3:ListBucket`, `s3:DeleteObject`).
- **Resources**: Specifies which buckets or objects the policy applies to (e.g., `"arn:aws:s3:::my-bucket/*"`).
- **Principals**: Defines who the policy applies to (e.g., a specific user, role, or account).
- **Conditions**: Optional constraints under which the policy is applied (e.g., IP address, multi-factor authentication).

#### Key Features
- **Fine-Grained Control**: Allows precise control over S3 resources at the bucket and object level.
- **Cross-Account Access**: Enables secure sharing of S3 resources across AWS accounts.
- **Conditional Access**: Policies can include conditions like IP addresses, VPC, or encryption status to further secure access.

#### Example
This is an example of a simple `JSON` bucket policy that grants read-only access to all objects in a specific `S3` bucket to anyone (public access):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-bucket-name/*"
    }
  ]
}
```
**Explanation:**  
- **Version**: Specifies the policy language version. `2012-10-17` is the latest version.
- **Statement**: The core component of the policy.
- **Effect**: Specifies whether the policy allows or denies access. In this case, it’s `Allow`.
- **Principal**: Defines who has access. `*` allows access to anyone (public access).
- **Action**: Specifies the `S3` operation that is allowed. Here, `s3:GetObject` allows read-only access to the objects.
- **Resource**: Specifies which bucket or objects this policy applies to. `arn:aws:s3:::my-bucket-name/*` refers to all objects (/*) within the bucket `my-bucket-name`.

These policies ensure that `S3` access is both flexible and secure, adhering to the principle of least privilege.


## S3 – Static Website Hosting

**Amazon S3** allows you to host static websites directly from an `S3` bucket. This feature is designed for websites that consist of static content like HTML, CSS, JavaScript, and media files, without the need for server-side scripting or dynamic content.

### Key Features:
- **Easy Setup**: You can configure an `S3` bucket to serve static website content by enabling static website hosting and specifying an index document (e.g., `index.html`) and an optional error document (e.g., `404.html`).
- **Custom Domain**: `S3` can be used to host websites under a custom domain by routing traffic through `Amazon Route 53` or another DNS provider.
- **Scalability and Availability**: `S3` automatically scales to handle any level of traffic, ensuring high availability without managing infrastructure.
- **Cost-Effective**: Pay only for the storage used and data transferred, making it a cost-efficient solution for static website hosting.

### Steps to Enable Static Website Hosting:
1. **Create an S3 Bucket**: The bucket name should match your domain name if you're using a custom domain.
2. **Enable Static Website Hosting**: In the `S3` bucket settings, enable static website hosting and specify the index and error documents.
3. **Upload Content**: Add your static files (HTML, CSS, JavaScript, images) to the bucket.
4. **Make Files Public**: Set the appropriate permissions for your files so they can be publicly accessible.
5. **Optional**: Configure your domain with `Route 53` to route traffic to your `S3` bucket.

### Example Use Cases:
- Hosting personal blogs, portfolios, or documentation.
- Serving static landing pages or marketing websites.
- Storing and delivering web resources (e.g., images, scripts) for other web applications.

`S3` static website hosting is a powerful, low-maintenance solution for serving static content with minimal effort.


## S3 – Versioning

**Amazon S3 Versioning** is a feature that allows you to keep multiple versions of an object in a bucket. When versioning is enabled, every time an object is modified or deleted, `S3` preserves the previous versions, allowing you to recover or restore earlier states of the object.

### Key Features:
- **Protects Data**: Helps prevent accidental overwrites and deletions by retaining object history.
- **Object Recovery**: You can restore previous versions of objects at any time.
- **Version ID**: Each version of an object is assigned a unique Version ID.

>> * Any file that existed before versioning was enabled will have a version ID of "null".  
>> * Suspending versioning does not remove existing versions; all previous versions are retained.

Versioning is especially useful for backup, recovery, and ensuring data integrity.