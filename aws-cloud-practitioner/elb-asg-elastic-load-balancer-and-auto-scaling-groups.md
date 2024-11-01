# ELB & ASG - Elastic Load Balancing and Auto Scaling Groups 

![AWS ELB & ASG - Elastic Load Balancing](/aws-cloud-practitioner/imgs/Res_Elastic-Load-Balancing_Application-Load-Balancer_48.png)

<!-- TOC depthFrom:2 -->
- [Summary](#summary)
- [ELB - Elastic Load Balancing](#elb---elastic-load-balancing)
- [ASG - Auto Scaling Groups](#asg---auto-scaling-groups)
- [Scalability and High Availability](#scalability-and-high-availability)

<!-- /TOC -->

## Summary

* **High Availability vs Scalability vs Elasticity vs Agility in the Cloud**:
  * **High Availability**: Ensures continuous operation with minimal downtime.
  * **Scalability**: Ability to handle increased loads (`Vertical`: adding resources to a single instance, `Horizontal`: adding more instances).
  * **Elasticity**: Automatic adjustment of resources based on real-time demand.
  * **Agility**: Quickly provisioning new IT resources to reduce time for development.

* **ELB - Elastic Load Balancers**:
  * Distribute traffic across backend `EC2` instances, supporting `Multi-AZ` deployments.
  * Support health checks to ensure traffic is routed only to healthy instances.
  * Four types:
    * **Classic Load Balancer (`CLB`)**: Legacy option, supports both L4 and L7.
    * **Application Load Balancer (`ALB`)**: Operates at Layer 7 (HTTP/HTTPS).
    * **Network Load Balancer (`NLB`)**: Operates at Layer 4 (TCP).
    * **Gateway Load Balancer (`GLB`)**: Operates at Layer 3, integrates with virtual appliances.

* **ASG - Auto Scaling Groups**:
  * Implement elasticity for your application across multiple AZs.
  * Scale `EC2` instances based on demand, automatically replacing unhealthy instances.
  * Integrated with `ELB` for seamless traffic distribution and scaling.



## ELB - Elastic Load Balancing

**ELB - Elastic Load Balancing** automatically distributes incoming traffic across multiple targets (`EC2` instances, containers) to ensure high availability and reliability.

### Key Features:
- **High Availability**: Spreads traffic across multiple Availability Zones.
- **Health Monitoring**: Routes traffic only to healthy targets.
- **Scalability**: Adjusts to varying traffic loads.
- **Security**: Supports SSL/TLS termination and integrates with AWS WAF.
- **Types of ELBs**:
    - **Application Load Balancer (ALB)**: Operates at Layer 7 (HTTP, HTTPS only).
    - **Network Load Balancer (NLB)**: Operates at Layer 4, designed for ultra-high performance and supports TCP.
    - **Gateway Load Balancer (GLB)**: Operates at Layer 3, integrates with third-party virtual appliances, route traffic to firewalls, intrusion detection.
    - **Classic Load Balancer (CLB)**: Operated at both Layer 4 and Layer 7, `retired in 2023.

- **Examples**:
    - Distributes traffic across multiple downstream instances.
    - Exposes a single point of access (DNS) to an application.
    - Performs regular health checks on instances.
    - Provides SSL termination (HTTPS) for secure websites.  

## ASG - Auto Scaling Groups

**ASG - Auto Scaling Groups** maintain the desired number of `EC2` instances to match application demand, ensuring optimal performance and cost efficiency.

### Key Features:
- **Automatic Scaling**: Adds or removes instances based on demand.
- **Health Checks**: Monitors and replaces unhealthy instances.
- **Desired Capacity**: Keeps the specified number of instances running.
- **ELB Integration**: Works with `ELB` to distribute traffic across instances.


### Scaling Strategies

* **Manual Scaling**: Manually adjust the size of the Auto Scaling Group (`ASG`) as needed.

* **Dynamic Scaling**: Automatically adjusts to changing demand.
  * **Simple / Step Scaling**:
    * Triggered by CloudWatch alarms, e.g., add 2 units when CPU > 70%, remove 1 unit when CPU < 30%.
  * **Target Tracking Scaling**:
    * Maintains the average `ASG` CPU usage around a specific target, e.g., 40%.
  * **Scheduled Scaling**:
    * Anticipates scaling based on known usage patterns.
    * Example: Increase the `min` capacity to X at 5 PM on Fridays.
  * **Predictive Scaling**:
    * Uses Machine Learning to predict future traffic.
    * Automatically provisions the appropriate number of EC2 instances in advance.
    * Useful for loads with predictable, time-based patterns.

Together, `ELB` and `ASG` provide a scalable, highly available, and fault-tolerant infrastructure for your applications.


## Scalability and High Availability

### Scalability
The ability of an application to handle increased loads by adapting appropriately.

#### Types of Scalability
* **Vertical Scalability**
* **Horizontal Scalability (Elasticity)**

#### Scalability vs. High Availability
While related, they are distinct concepts; `scalability` refers to handling increased loads, whereas `high availability` ensures continuous 
operational performance.

### Vertical Scalability

* **Definition**: Increasing the size or capacity of a single instance.
* **Example**: Upgrading from a `t2.micro` to a `t2.large`.
* **Use Case**: Common for non-distributed systems like databases.
* **Limitations**: Limited by the maximum hardware capacity of the instance.

### Horizontal Scalability

* **Definition**: Adding more instances to distribute the load.
* **Example**: Adding more servers to a web application to handle more traffic.
* **Use Case**: Suitable for distributed systems and cloud environments.
* **Benefits**: No single point of failure and can scale indefinitely with more instances.


#### Scalability vs. Elasticity vs. Agility

#### Elasticity
- **Definition**: The ability of a system to automatically adjust its resources to match the current load in real-time.
- **Characteristics**:
    - **Automatic Scaling**: Resources scale in or out based on demand without manual intervention.
    - **Cost Efficiency**: Optimizes resource usage, scaling down when demand decreases to save costs.
- **Goal**: Provide real-time resource adjustment to handle varying workloads efficiently.

### Key Differences
- **Scalability** is about the system's ability to grow and handle increased load.
- **Elasticity** is about the system's ability to automatically adjust resources in real-time based on the load.
- **Agility**: Not directly related to scalability, but refers to the ability to quickly provision new IT resources. This means that resources are just a click away, significantly reducing the time required to make them available to your developers.
