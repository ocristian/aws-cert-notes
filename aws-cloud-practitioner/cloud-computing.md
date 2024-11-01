# AWS Cloud Practitioner - CLF-C02 exam

<!-- TOC depthFrom:2 -->
- [Cloud Computing](#cloud-computing)
    * [Deployment Models](#deployment-models)
    * [Characteristics of Cloud Computing](#characteristics-of-cloud-computing)
    * [Advantages of Cloud Computing](#advantages-of-cloud-computing)
    * [Problems solved by the Cloud](#advantages-of-cloud-computing)
    * [Different Types of Cloud Computing](#different-types-of-cloud-computing)
    * [AWS Cloud History](#aws-cloud-history)
    * [AWS Global Infrastructure](#aws-global-infrastructure)
    * [Shared Responsibility Model and AWS Acceptable Policy](#shared-responsibility-model-and-aws-acceptable-policy)
<!-- /TOC -->

<a name="cloud-computing"></a>
## Cloud Computing

Cloud computing is the `on-demand delivery` of compute power, database storage, applications, and other IT resources.
Resources can be provisioned in the exact type and size of computing needed, and you pay as it go, only for what you use.

AWS (Amazon Web Services) owns and maintains the network-connected hardware required for these application services, while you provision and use what you need via a web
application.

<a name="deployment-models"></a>
### Deployment Models
#### Private Cloud
* Cloud services used by a single organization, not exposed to the public.
* Complete control
* Security for sensitive applications
* Meet specific business needs

#### Public Cloud
* Cloud resources owned and operated by a third-party cloud service provider delivered over the Internet.

#### Hybrid Cloud
* Keep some servers on premises and extend some capabilities to the Cloud
* Control over sensitive assets in your private infrastructure
* Flexibility and cost-effectiveness of the public cloud

<a name="characteristics-of-cloud-computing"></a>
### Characteristics of Cloud Computing
#### On-demand self-service
* Users can provision resources and use them without human interaction from the service provider

#### Broad network access
* Resources available over the network, and can be accessed by diverse client platforms

#### Multi-tenancy and resource pooling
* Multiple customers can share the same infrastructure and applications with security and privacy
* Multiple customers are serviced from the same physical resources

#### Rapid elasticity and scalability
* Automatically and quickly acquire and dispose resources when needed
* Quick and easily scale based on demand

#### Measured service
* Usage is measured, users pay correctly for what they have used

<a name="advantages-of-cloud-computing"></a>
### Advantages of Cloud Computing
#### Trade capital expense (CAPEX) for operational expense (OPEX)
* Pay on-demand, don't own hardware
* Reduced Total Cost of Ownership (TCO) and Operational Expense (OPEX)

#### Benefit from massive economies of scale
* Prices are reduced as AWS is more efficient due to large scale

#### Stop guessing capacity
* Scale based on actual measured usage

#### Increase speed and agility

#### Stop spending money running and maintaining data centers

#### Go global in minutes: leverage the AWS global infrastructure

<a name="problems-solved-by-the-cloud"></a>
### Problems solved by the Cloud
* `Flexibility`: change resource types when needed
* `Cost-Effectiveness`: pay as you go, for what ou use
* `Scalability`: accommodate larger loads by making hardware stronger or adding additional nodes
* `Elasticity`: ability to scale-out and scale-in when needed
* `High-availability` and `fault-tolerance`: build across data centers
* `Agility`: rapidly develop, test and launch software applications

<a name="different-types-of-cloud-computing"></a>
### Different Types of Cloud Computing

#### IaaS - Infrastructure as a Service
* Provides networking, computers, data storage space
* Highest level of flexibility
* Easy parallel with traditional on-premises IT

#### PaaS - Platform as a Service
* Removes the need for your organization to manage the underlying infrastructure
* Focus on the deployment and management of your application

#### SaaS - Software as a Service
* Completed product that is run and managed by the service provider

#### Management on each Cloud Type
* Managed by you

| On-premises    | IaaS - Infrastructure<br/>as a Service | PaaS - Platform<br/>as a Service | SaaS - Software<br/>as a Service |
|----------------|----------------------------------------|----------------------------------|----------------------------------|
| Applications   | Applications                           | Applications                     |                                  |
| Data           | Data                                   | Data                             |                                  |
| Runtime        | Runtime                                |                                  |                                  |
| Middleware     | Middleware                             |                                  |                                  |
| OS             | OS                                     |                                  |                                  |
| Virtualization |                                        |                                  |                                  |
| Servers        |                                        |                                  |                                  |
| Storage        |                                        |                                  |                                  |
| Networking     |                                        |                                  |                                  |

* Managed by others

| On-premises | IaaS - Infrastructure<br/>as a Service | PaaS - Platform<br/>as a Service | SaaS - Software<br/>as a Service |
|-------------|----------------------------------------|----------------------------------|----------------------------------|
|             | Virtualization                         | Runtime                          | Application                      |
|             | Servers                                | Middleware                       | Data                             |
|             | Storage                                | OS                               | Runtime                          |
|             | Networking                             | Virtualization                   | Middleware                       |
|             |                                        | Servers                          | OS                               |
|             |                                        | Storage                          | Virtualization                   |
|             |                                        | Networking                       | Servers                          |
|             |                                        |                                  | Storage                          |
|             |                                        |                                  | Networking                       |

#### Examples of Cloud Computing Types
* IaaS - Infrastructure as a Service
    * Amazon EC2 on AWS
    * GCP, Azure

* PaaS - Platform as a Service
    * Elastic Beanstalk on AWS
    * Heroku, Google App Engine on GCP, Windows Azure on Microsof
* SaaS - Software as a Service
    * AWS Services as Rekognition for Machine Learning
    * Google Apps as Gmail and Photos, Zoom, Dropbox

#### Pricing
* AWS has 3 pricing fundamentals, following the pay-as-you-go pricing model
    * Compute: Pay for compute time
    * Storage: Pay for data stored in the Cloud
    * Data Transfer OUT of the Cloud: Data transfer IN is free

<a name="aws-cloud-history"></a>
### AWS Cloud History

```mermaid
timeline
2002 : Launched as amazon.com
2003 : Idea to offer IT to the market
2004 : SQS - 1st available to the public
2006 : SQS, EC2 and S3
2007 : Launched in Europe
```

<a name="aws-global-infrastructure"></a>
### AWS Global Infrastructure
#### AWS Regions
* Each regions is connected thru private AWS network
* Are all around the world
* Names can be `us-east-1`, `eu-west-3`
* A region is a `cluster of data centers`
* Most AWS services are region-scoped

##### How to choose an AWS Regions?
* `Compliance` with data governance and legal requirements: data never leaves a region without explicit permission
* `Proximity` to customers: reduced latency
* `Available services` within a region: new services and features aren't available in every region
* `Pricing` varies region to region

#### AWS Availability Zones
* Each region has many availability zone, usually 3, min is 3 and max is 6
    * Example: `eu-west-1a`, `eu-west-1b` and `eu-west-1c`
* Each `AZ` - availability zone is one or more discrete data centers with redundant power, networking and connectivity
* `AZs` are separate from each other, isolated from disaster
* `AZs` are connected with high bandwidth, ultra-low latency networking

#### AWS Global Services
* `IAM` - Identity and Access Management
* `Route 53` - DNS service
* `CloudFront` - Content Delivery Network
* `WAF` - Web Application Firewall

##### Most AWS Services Region-scoped
* `Amazon EC2` - Infrastructure as a Service
* `Elastic Beanstalk` - Platform as a Service
* `Lambda` - Function as a Service
* `Rekognition` - Software as a Service

<a name="shared-responsibility-model-and-aws-acceptable-policy"></a>
### Shared Responsibility Model and AWS Acceptable Policy
* `Customer` responsibility for the security `IN` the cloud
* `AWS` responsibility for the security `OF` the cloud

<img alt="AWS Shared Responsibility Model" src="https://d1.awsstatic.com/security-center/Shared_Responsibility_Model_V2.59d1eccec334b366627e9295b304202faf7b899b.jpg">