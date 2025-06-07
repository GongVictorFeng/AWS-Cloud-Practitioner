# AWS-Cloud-Practitioner

## Before the Cloud 
Example 1 - Online Shopping APP
* Challenge: 
  * Peak usage during holidays and weekends
  * Less load during rest of the time
* Solution (before the Cloud):
  * Procure (Buy) infrastructure for peak load
    * the infrastructure would be idling during period of low loads

Example 2 - Startup
* Challenge:
  * It suddenly becomes popular
  * How to handle the sudden increase in load
* Solution (before the Cloud):
  * Procure (Buy) infrastructure assuming they would be successful
    * what if they are not successful

Challenges before the Cloud:
  * High costs of procuring infrastructure
  * Needs ahead of time planning (hard to predict the future)
  * Low infrastructure utilization
  * Dedicated infrastructure maintenance team (Startup usually can not afford)

## Silver lining in the Cloud
On-demand resource provision - also called Elasticity
* Advantages:
  * Trade "capital expense" for "variable expense"
  * Benefit from massive economies of scale
  * Stop guessing capacity
  * Increase speed and agility
  * Stop spending money running and maintaining data centers
  * "Go global" in minutes

## Regions and Zones
* Imagine that your application is deployed in a data center in London
* What would be the challenges?
  * Slow access for users from other parts of the world (high latency)
  * What if the data center crashes
    * Your application goes down (low availability)

Multiple data centers
* Let's add in one more data center in London
* What would be the challenges?
  * Slow access for users from other parts of the world
  * Solved: What if one data center crashes?
    * Your application is till available from the other data center
  * What if the entire region of London is unavailable?
    * Your application goes down

Multiple regions
* Let's add a new region: Singapore
* What would be the challenges?
  * Partly solved: Slow access for users from other parts of the world
  * Solved: What if one data center crashes?
  * Solved: What if the entire region of London is unavailable
    * Your application is served from Singapore

Regions
* Imagine setting up your own data centers in different regions around the world
* AWS provides 20+ regions around the world (expanding every year)
* Advantages:
  * Low Latency
  * Global Footprint
  * Adhere to government regulations
  * High Availability

Availability Zones
* Each AWS Region consists of multiple, isolated and physically separated availability zones
* Availability zones in a region are connected through low-latency links
* Each Availability zone:
  * Can have one or more discrete data centers
  * Has redundant power, networking, and connectivity
* (Advantage) Increase availability and fault tolerance of applications in the same region

## EC2 (Elastic Compute Cloud)
* In corporate data centers, applications are deployed to physical servers
* Where do you deploy applications in the cloud
  * Rent virtual servers
  * EC2 instances - Virtual servers in AWS
  * EC2 service - Provision EC2 instances or virtual servers

EC2 Features
* Create and manage lifecycle of EC2 instances
* Attach storage (& network storage) to your EC2 instances
* Manage network connectivity for an EC2 instance
* Load balancing and auto-scaling for multiple EC2 instances

Useful Commands
* `sudo su` be a super-user
  * make the user the root which has complete access to the entire EC2 instance
  * can install software
* `yum update -y` ensure all the packages are upto date
* `yum install httpd` install Apache web server
* `systemctl start httpd` start the web server
* `systemctl enable httpd` enable httpd to be started on restarting the EC2 instance
* `echo "Hello World" > /var/www/html/index.html` write Hello World to the file

EC2 Concepts - AMI - Amazon Machine Image
* What operating system and what software do you want on the instance
* Three AMI sources:
  * Provided by AWS
  * AWS Market Place: Online store for customized AMIs. Per hour billing
  * Customized AMIs: Created by you

EC2 Concepts - Instance Families
* Optimized combination of compute (CPU, GPU), memory, disk (storage) and networking for specific workloads
* 270+ instances across 40+ types for different workloads
  * m (m4, m5, m6) - General Purpose
  * c (c4, c5, c5n) - Compute Optimized
  * r (r4, r5, r5a, r5n) - Memory (RAM) optimized
  * i (i3) - Storage (I/O) optimized
  * g (g3, g4) - GPU Optimize - Graphics Processing

EC2 Concepts - Security Groups
* Virtual firewall to control incoming and outgoing traffic to/from AWS resources (EC2 instances, databases etc)
* Provides additional layer of security - Defense in Depth
* Rules:
  * Default deny - If there are no rules configured, no outbound/inbound traffic is allowed
  * Allows allowing rules only
  * Separated rules for inbound and outbound traffic

EC2 Security - Key Pairs
* EC2 uses public key cryptography for protecting login credentials
* Key pair -public key and private key
  * Public key is stored in EC2 instance
  * Private key is stored by customer
* for SSH connection

EC2 IP Addresses
* Public IP addresses are internet addressable 
* Private IP addresses are internal address in a corporate network
* You can not have two resources with the same public IP address
* However, two different corporate networks can have resources with the same private IP address
* All EC2 instances are assigned private IP addresses
* when the EC2 instance is stopped, the public IP address is lost

Elastic IP Address
* a constant public IP address for a EC2 instance
* Elastic IP can be switched to another EC2 instance within the same region
* Elastic IP remains attached even if you stop the instance. You have to manually detach it
* You are charged for an Elastic IP when you are NOT using it! Make sure that you explicitly release an Elastic IP when you are not using it

IAAS (Infrastructure as a Service)
* Use only infrastructure from cloud provider
  * Computers (virtual or on dedicated hardware), data storage space and Networking features
* Also called "Lift and Shift"
* Example: Use EC2 to deploy application
* Example: Use EC2 to create database
* Cloud Provider is responsible for:
  * Physical infrastructure (Hardware, Networking)
  * Virtualization Layer (Hypervisor, Host OS)
* Customer is responsible for:
  * Guest OS upgrades and patches
  * Application code and Runtime
  * Application configuration: Availability, Fault Tolerance, Scalability etc

PAAS (Platform as a Service)
* Use a platform provided by cloud
* Cloud provider is responsible for:
  * OS (including upgrades and patches)
  * Application Runtime
  * Auto scaling, Availability & Load balancing etc
* Customer is responsible for:
  * Application code
  * Configuration
* Examples:
  * AWS Managed Service
    * Elastic Load Balancing - Distribute incoming traffic across multiple targets
    * AWS Elastic Beanstalk - Run and Manage Web Apps
    * Amazon RDS - Relational Databases - MSQL, Oracle, SQL server etc

Elastic Load Balancer
* Distribute traffic across EC2 instances in one or more AZs in a single region
* Managed service - AWS ensures that it is highly available
* Auto-scales to handle huge load
* Load Balancers can be public or private
* Health checks - route traffic to healthy instances
* Four types of Elastic Load Balancers
  * Classic Load Balancer (Layer 4 and Layer 7)
    * Old generation supporting layer 4 (TCP/TLS) and layer 7(HTTP/HTTPS) protocols
    * Not Recommended by AWS
  * Application Load Balancer (layer 7)
    * Most popular and frequently used ELB in AWS
    * New generation supporting HTTP?HTTPS
    * Supports advanced routing approaches (Headers, Query Params, Path and Host Based)
  * Network Load Balancer (Layer 4)
    * New generation supporting TCP/TLS and UDP
    * Very high performance use cases
  * Gateway Load Balancer
    * Use to deploy, scale and run third-party virtual application on AWS
    * Distribute traffic across multiple virtual appliances, providing a single entry point for all traffic while offering scalability and increased availability

Availability 
* The applications available when the users need them
* Percentage of time - an application provides operation expected of it
* Example:
  * Availability - 99.95%, Downtime (in a month) - 22 minutes
  * Availability - 99.99%, Downtime (in a month) - 4.5 minutes, most online apps aim for 99.99% (four 9's)
  * Availability - 99.999%, Downtime (in a month) - 26 seconds, achieving 5 9's is tough
* Increase Availability:
  * Deploy to multiple AZs
  * Deploy to multiple regions

Scalability 
* A system is handling 1000 transactions per second. Load is expected to increase 10 times in the next month
  * can we handle a growth in users, traffic, or data size without any drop in the performance?
  * Does ability to server more growth increase proportionally with resources
* Ability to adapt to changes in demand (users, data)
* What are the options that can be considered
  * Deploy to a bigger instance with bigger CPU and more memory
  * Increase the number of application instances and set up a load balancer
* Vertical Scaling
  * Deploying application/database to bigger instance:
    * A larger hard drive
    * A faster CPU
    * More RAM, CPU, I/O, or networking capabilities 
  * There are limits to vertical scaling
  * Vertical Scaling for EC2
    * Increasing EC2 instances size:
      * t2.micro to t2.small
      * t2.small to t2.2xlarge
* Horizontal Scaling
  * Deploying multiple instances of application/database
  * (Typically but not always) Horizontal Scaling is preferred to Vertical Scaling
    * Vertical scaling has limits
    * Vertical scaling can be expensive
    * Horizontal scaling increases availability
  * (BUT) Horizontal Scaling needs additional infrastructure
    * Load Balancers etc
  * Horizontal Scaling for EC2:
    * Distribute EC2 instances
      * in a single AZ
      * in multiple AZs in single region
      * in multiple AZs in multiple regions
    * Auto scale: Auto Scaling Group
    * Distribute load: Elastic Load Balancer

EC2 Tenancy - Shared vs Dedicated
* Shared Tenancy (Default)
  * Single host machine can have instances from multiple customers
* EC2 Dedicated Instances
  * Virtualized instances on hardware dedicated to one customer
  * You do not have visibility into the hardware of underlying host
* EC2 Dedicated Hosts
  * Physical servers dedicated to one customer
  * You have visibility into the hardware of underlying host (socket and physical cores)
  * (Use cases) Regulatory needs or server-bound software licenses like Windows Server, SQL Server

EC2 Pricing Models Overview
* On Demand
  * Request when you want it
  * Flexible and Most expensive
* Spot
  * Quote the maximum price
  * Cheapest (upto 90% off) but no guarantees
* Reserved
  * Reserve ahead of time
  * Upto 75% off. 1 or 3 years reservation
* Saving plans
  * Commit spending $X per hours on (EC2 or AWS Fargate or Lambda)
  * Upto 66% off. No restrictions. 1 or 3 years reservation

EC2 On-Demand
* On demand resource provisioning - Use and Throw
* Highest cost and highest flexibility
* Ideal for:
  * A web application which receives spiky traffic
  * A batch program which has unpredictable runtime and can not be interrupted
  * A batch program being move from on-premises to cloud for the first time

EC2 Spot instances
* (Old Model) Bid a price. Highest bidder wins
* (new Model) Quote your maximum price. Prices decided by long term trends
* Up to 90% off 
* Can be terminated with a 2 minutes notice
* Ideal for Non-time-critical workloads that can tolerant interruptions (fault-tolerance)
  * A batch program that does not have a strict deadline and can be stopped at short notice and re-started

EC2 Reserved Instances
* Reserve EC2 instances ahead of time
* Get upto 75% off
* Payment models
  * No Upfront - $0 upfront. Pay monthly installment
  * Partial Upfront - $XYZ upfront. Pay monthly installment
  * Partial Upfront - $XYZ upfront. Pay monthly installment
  * Cost wise : Earlier you pay, more the discount. All Upfront < Partial Upfront < No Upfront

EC2 Saving Plans
* EC2 Compute Savings Plans
  * Commitment: I would spend X dollars per hour on AWS compute resources (Amazon EC2 instances, AWS Fargate and/or AWS Lambda) for a 1 or 3 years period
  * Upto 66% off
  * Provides complete flexibility:
    * You can change instance family, size, OS, tenancy or AWS Region of your Amazon EC2 instances
    * You can switch between Amazon EC2, AWS Fargate and/or AWS lambda
* EC2 instance Saving Plans
  * Commitment: I would spend c dollars per hour on Amazon EC2 instances of a specific instance family (General Purpose, for example) within a specific region
  * Upto 72% off
  * You can switch operating systems