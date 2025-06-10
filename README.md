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

## ELB (Elastic Load Balancer)
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

## Elastic BeanStalk
* Next level of platform as a service (paas)
* Simplest way to deploy and scale your web application in AWS
  * Provides end-to-end web application management
* Supports Java, .Net, Node.js, PHP, Ruby, Python, Go and Docker application
* No usage charge - Pay for AWS resource provisioned
* Features:
  * Automatic load balancing
  * Auto scaling
  * Managed platform updates
  * Application health monitoring

AWS Elastic Beanstalk Concepts
* Application - A container for environments, versions and configuration
* Application Version - A specific version of deployable code
* Environment - An application version deployed to AWS resources. You can have multiple environments running different application version for the same application

Auto Scaling Components
* Launch Configuration/Template (What?)
  * EC2 instance size and AMI
* Auto Scaling Group (Where?)
  * Min, max and desired size of ASG
  * Health checks
* Auto Scaling Policies (When?)
  * When and How to execute scaling

Dynamic Scaling Policy Types
* Target tracking scaling 
  * Modify current capacity based on a target value for a specific metric
  * Example: Maintain CPU utilization at 70%
* Simple scaling 
  * Waits for cool-down period before triggering additional actions
  * Example: +5 if CPU utilization > 80%; -3 if CPU utilization < 60%
* Step scaling
  * Warm up time can be configured for each instance
  * Example:  +1 if CPU utilization between 70% and 80%;  
    +3 if CPU utilization between 80% and 100%  
    Similar settings for scale down
* Scaling Policies - Background
  * CloudWatch alarm (Is CPU utilization >80%? or < 60%)
  * Scaling action ((+5 EC2 instances or -3 EC2 instances)

## Serverless
* A concept of focusing on building application without worrying about servers
* What are the things we think about while developing an application
  * Where do we deploy the application
  * What kind of server? What OS
  * How do we take care of scaling the application
  * How do we ensure that it is always available
* Serverless does not mean "No Servers"
  * Do not worry about infrastructure
  * Flexible scaling 
  * Automated high availability
  * Pay for use:
    * You don't have to provision servers or capacity
  * focus on code and the cloud managed service takes care of all that is needed to scale the code to server millions of requests

AWS Lambda - the most popular serverless service
* World before Lambda - ELB with EC2 servers
* Do not worry about servers or scaling or availability
* Focus on code
* Pay for what use
  * Number of requests
  * Duration of requests
  * Memory consumed
* Supported lots of programming languages
* AWS Lambda Event Sources: Amazon API Gateway, AWS Cognito,  Amazon DynamoDB (event), Amazon CloudFront (Lambda@Edge),  AWS Step Functions,...

## Amazon S3 (Simple Storage Service)
* Most popular, very flexible and inexpensive storage service
* Store large objects using a key-value approach
* Also called Object Storage
* Provides REST API to access and modify objects
* Provides unlimited storage:
  * (S3 storage class) 99.99% availability and (11 9's) durability
  * Objects are replicated in a single region (across multiple AZs)
* Store all file types - text, binary, backup and archives:
  * Media files and archives
  * Application packages and logs
  * Backups of databases or storage devices
  * Staging data during on-premise to cloud database migration

Objects and Buckets
* Amazon S3 is a global service. Not associated with a region
  * However, a bucket is created in a specific AWS region
* Objects are stored in buckets
  * Bucket names are globally unique
  * Bucket names are used as part of object URLs => Can contain only lower case letters, numbers, hyphens and periods
  * Unlimited objects in a bucket
* Each object is identified by a key value pair
  * Key is unique in a bucket
  * Max object size is 5 TB

Amazon S3 Storage Classes 
* Different kinds of data can be stored in Amazon S3
  * Media files and archives
  * Application packages and logs
  * Backups of the databases or storage devices
  * Long term archives
* Huge variations in access patterns
* Trade-off between access time and cost
* S3 storage classes help optimize costs while meeting access time needs
* Storage Class:
  * Standard - Frequently accessed data, >= 3 AZs
  * Standard-IA - Long-lived, infrequently accessed data (backups for disaster recovery), >= 3 AZs
  * One Zone-IA - Long-lived, infrequently accessed, non-critical data (Easily re-creatable data - thumbnails for images), 1 AZs
  * Intelligent-Tiering - Long-lived data with changing or unknown access patterns, >= 3 AZs
  * Glacier - Archive data with retrieval times ranging from minutes to hours, >= 3 AZs
  * Glacier Deep Archive - Archive data that rarely, if ever, needs to be accessed with retrieval times in hours
  
Amazon S3 Cost
* Important pricing elements:
  * Cost of Storage (per GB)
  * (If Applicable) Retrieval Charge (per GB)
  * Monthly tiering fee (Only for intelligent Tiering)
  * Data transfer fee
* Free of cost:
  * Data transfer into Amazon S3
  * Data transfer from S3 to Amazon CloudFront
  * Data transfer from S3 to services in the same region

Amazon S3 Glacier
* In addition to existing as a S3 Storage class, S3 Glacier is a separate AWS service on it own
* Extremely low cost storage for archives and long-term backups:
  * Old media content
  * Archives to meet regulatory requirements (old patient records,...)
  * As a replacement for magnetic tapes
* High durability (11 9's)
* High scalability (unlimited storage)
* High security (encrypted at rest and in transfer)

Amazon S3 vs S3 Glacier
* Terminology:
  * Amazon S3 - Objects (files) are stored in Buckets (container)
  * S3 Glacier - Archives (files) are stored in Vaults (containers)
* Keys
  * S3 - Objects keys are user defined
  * S3 Glacier - Archive keys are system generated identifiers
* Mutability
  * S3 - (Default) Allows uploading new content to object
  * S3 Glacier - after an archive is created, it cannot be updated (Perfect for regulatory compliance)
  * Max size
    * S3 - Each object can be upto 5TB
    * S3 Glacier - Each archive can be upto 40TB
  * Encryption
    * S3 - Optional
    * S3 Glacier - mandate

## Storage Types - Block Storage and File Storage
* What is the type of storage of the hard disk
  * Block Storage
* You've created a file share to share a set of files with your colleagues in a enterprise. What type of storage are you using
  * File Storage

Block Storage
* Use case: Hard-disks attached to your computers
* Typically, One Block Storage device can be connected to one virtual server
* However, you can connect multiple different block storage devices to one virtual server

File Storage
* Media workflows need huge shared storage for supporting processes like video editing
* Enterprise users need a quick way to share files in a secure and organized way
* These file shares are shared by several virtual servers

AWS - Block Storage and File Storage
* Block Storage:
  * Amazon Elastic Block Store (EBS)
  * Instance store
* File Storage:
  * Amazon EFS (for Linux instances)
  * Amazon FSx Windows File Servers
  * Amazon FSx for Lustre (high performance use cases)

EC2 -Block Storage
* Two popular types of block storage can be attached to EC2 instances:
  * Elastic Block Store (EBS)
  * Instance Store
* Instance Stores are physically attached to the EC2 instance
  * Temporary data
  * Lifecycle ties to EC2 instance
* Elastic Block Store (EBS) is network storage
  * More durable
  * Lifecycle Not ties to EC2 instance

Instance Store 
* Physically attached to EC2 instance
* Ephemeral storage
  * Temporary data
  * Data is lost when hardware fails or an instance is terminated
  * Use case: cache or scratch files
* Lifecycle is tied to EC2 instance
* Only some of the EC2 instance types support instance store
* Advantages:
  * Very Fast (2-100x of EBS)
  * No extra cost. Cost is included in the cost of EC2 instance
  * Ideal for storing temporary information - cache, scratch files,...
* Disadvantages
  * Slow boot up (up to 5 minutes)
  * Ephemeral storage (data is lost when hardware fails or instance is terminated)
  * Can not take a snapshot or restore from snapshot
  * Fixed size based on instance type
  * You cannot detach and attach it to another EC2 instance

Amazon Elastic Block Store (EBS)
* Network block storage attached to your EC2 instance
* Provisioned capacity
* Very flexible
  * Increase size when you need it - when attached to EC2 instance
* Independent lifecycle from EC2 instance
  * Attach/Detach from one EC2 instance to another
* 99.999% Availability & replicated within the same AZ
* Use case: Run your custom database
* Update:
  * Generally Block Storage devices can be connected to a single EC2 instance
  * Amazon EBS Multi-Attach enables to attach a single Provisioned IOPS SSD volume to up to 16 Nitro-based instances that are in the same AZ.

Hard Disk Drive vs Solid State Drive
* Performance - IOPS
  * HDD - Low
  * SSD - High
* Throughput
  * HDD - High
  * SSD - High
* Great at
  * HDD - Large sequential I/O operation
  * SSD - Small, Random I/O operation & Sequential I/O
* Recommended for
  * HDD - Large streaming or big data workloads
  * SSD - Transactional workloads
* Cost 
  * HDD - Low
  * SSD - Expensive
* Boot Volumes
  * HDD - Not recommended
  * SSD - Recommended

Amazon EFS
* Petabyte scale, Auto scaling, Pay for use shared file storage
* Compatible with Amazon EC2 Linux-based instances
* Use cases: Home directories, file share, content management
* Alternative - Amazon FSx for lustre
  * File system optimized for performance
  * High performance computing (HPC) and media processing use cases
  * Automatic encryption at-rest and in-transit
* Alternative - Amazon FSx Windows File Servers
  * Fully managed Windows file servers
  * Accessible from Windows, Linux and MacOS instance
  * Integrates with Microsoft Active Directory to support Windows-based environments and enterprises
  * Automatic encryption at-rest and in-transit

AWS Storage Gateway
* Hybrid storage (cloud + on premise)
* Unlimited cloud storage for on-premise software applications and users with good performance
* Storage Gateway and S3 Glacier encrypt data by default
* Three options
  * AWS Storage File Gateway
  * AWS Storage Tape Gateway
  * AWS Storage Volume Gateway
* AWS Storage File Gateway
  * Problem Statement: Large on-premise file share with terabytes of data
    * Users put files into file share and applications use the files
    * Managing it is becoming expensive
    * Move the file share to cloud without performance impact
  * AWS Storage File Gateway provides cloud storage for file shares
    * Files stored in Amazon S3 & Glacier
* AWS Storage Tape Gateway
  * Tape backups used in enterprises (archives)
    * Stored off-site - expensive, physical war and tear
  * AWS Storage Tape Gateway - Avoid physical tape backups
  * No change needed for tape backup infrastructure
  * Backup data to virtual tapes (actually, Amazon S3 & Glacier)
* AWS Storage Volume Gateway
  * Volume Gateway: Move block storage to cloud 
  * Automate backup and disaster recovery
  * Use cases: Backup and disaster recovery, Migration of application data
  * Option 1 - Cached (Gateway Cached Volumes):
    * Primary Data Store - AWS - Amazon S3
    * On-premise cache stores frequently accessed data
  * Option 2 - Stored (Gateway Stored Volumes)
    * Primary Data Store - On-Premises
    * Asynchronous copy to AWS
    * Stored as EBS snapshots

## Databases Primer
* Databases provide organized and persistent storage for data
* To choose between different database types, we need to understand:
  * Availability
  * Durability 
  * Consistency
  * Transactions etc

Database - Getting Started
* Imaging a database deployed in a data center in London
* challenges:
  * The database will go down if the data center crashes or the server storage fails
  * The data will be lost if the database crashes

Database - Snapshots
* Automate taking copy of the database (take a snapshot) every hour to another data center in London
* Challenges:
  * The database will go down if the data center crashes
  * Partially solved : the data will be lost if the database crashes
    * You can set up database from latest snapshot. But depending on when failure occurs, you can lose up to an hour of data
  * Database will be slow when you take snapshots

Database - Transaction Logs
* Adding transaction logs to database and create a process to copy it over to the second data center
* Challenges:
  * The database will go down if the data center crashes
  * Solved: the data will be lost if the data center crashes
    * You can set up database from latest snapshot and apply transaction logs
  * Database will be slow when taking the snapshots

Database - Add a Standby
* Adding a standby database in the second data center with synchronous replication
* Challenges:
  * Solved: the database will go down if the data center crashes
  * Solved: the data will be lost if the database crashes
  * Solved: Database will be slow when you take snapshots
    * Take snapshots from standby
    * Applications connecting to master will get good performance always.
