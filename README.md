# aws-certified-solutions-architect-associated-exam-notes

These notes are intend for quick review in preparation for the AWS Certified Solutions Architect – Associate
(SAA-C02) Exam.

## Technologies
### Compute
### Cost management
### Database
### Disaster recovery
### High availability
### Management and governance
### Microservices and component decoupling
### Migration and data transfer
### Networking, connectivity, and content delivery
### Security
### Serverless design principles
### Storage

## AWS services and features 

### Analytics

#### [Amazon Athena](https://aws.amazon.com/athena/?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc)

* Query and analyze data in S3 using standard SQL.
* Serverless model.
* Pay only for the queries you run - $5 per TB of data scanned,
* You can save from 30% to 90% on your per-query costs and get better performance by compressing, partitioning, and converting your data into columnar formats.

#### Amazon Elasticsearch Service (Amazon ES)

* Elasticsearch as a managed service.
* [Amazon OpenSearch Service](https://aws.amazon.com/opensearch-service/) is the successor to Amazon Elasticsearch Service

#### [Amazon EMR](https://aws.amazon.com/emr/)

* Amazon Elastic Map Reduce.
* Petabyte-scale data analytics.
* Run Apache Spak, Hive, Presto and other big data workloads.
* Runs on EC2 CLuster, Amazon EKS, AWS Outposrs or Amazon EMR Serverless.

#### [AWS Glue](https://aws.amazon.com/glue/?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc)

* Serverless ETL Platform.
* Provides visual and code-based interfaces.

#### [Amazon Kinesis](https://aws.amazon.com/kinesis/)

* Collect, process, and analyze real-time, streaming data.
* Ungest real-time data such as video, audio, application logs, website clickstreams, and IoT telemetry data.
* Fully managed, serverless infrastructure.
* Capabilities
  * Amazon Kinesis Video - securely stream video from connected devices to AWS for analytics, machine learning (ML,  and other processing.
  * Amazon Kinesis Data Streams - scalable and durable real-time data streaming service that can continuously capture gigabytes of data per second from hundreds of thousands of sources.
  * Amazon Kinesis Data Firehose - capture, transform, and load data streams into AWS data stores for near real-time analytics with existing business intelligence tools.
  * Amazon Kinesis Data Analytics - process data streams in real time with SQL or Apache Flink without having to learn new programming languages or processing frameworks.

#### [Amazon QuickSight](https://docs.aws.amazon.com/quicksight/latest/user/welcome.html)

* Serverless BI Service.
* BI Dashboards, querying, data analysis, anomaly detection, what if, forcasting etc.

### AWS Billing and Cost Management

#### [AWS Budgets](https://aws.amazon.com/aws-cost-management/aws-budgets/)

* Planning & Cost control.
* Billing thresholds and alerts.
* Custom actions can be executed in response to billing alerts, automatically or with approval.

#### [Cost Explorer](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/)

* Visualise, understand and manage AWS costs and usage over time.
* Can use ML to forcast costs.

### Application Integration

#### Amazon Simple Notification Service (Amazon SNS)

* [Simple Notification Service](https://aws.amazon.com/sns/?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc)
* Fully managed messaging service that allows push notifications, SMS messages or email.
* Allows for many-to-many messaging between distributed systems.
* Can group recipients through topics.
* Highly available as all messages stored across multiple regions.
* PUSH based delivery.
* Pay as you go, no up front costs.

#### Amazon Simple Queue Service (Amazon SQS)

* [Simple Queue Service](https://aws.amazon.com/sqs/)
* Fully Managed Queue Service.
* Decouple applications, reduce system complexity with managing and operating message-oriented architectures.
* 2 Types of queues:
  * Standard
    * Default queue type.
    * Nearly unlimited API calls per second.
    * Guarantees message delivery AT LEAST once - can be more and occasionally out of order.
  * FIFO
    * First in, First out.
    * High Throughtput, up to 3K transaction per API batch call.
    * Processed once only, no duplicates.
    * Order is respected.
* Pull based, i.e. an application needs to pull the messages from the queue.
* *Visibility Timeout* - the amount of time the message is invisible in the queue after reader picks it up. It prevents other consumers from receiving and processing the same message. The message is then deleted. If the job hasn’t completed it becomes visible in the queue again (can be max 12 hours).
* If you are getting messages delivered twice, the cause could be your visibility timeout is too low. i.e. The application processing the messages takes a while.
* *Short Polling* — Keeps polling queue looking for work, even if it’s empty. You can introduce long polling as a way of reducing costs. [Amazon SQS short and long polling](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-short-and-long-polling.html)

### Compute

#### Amazon EC2

* Amazon's Virtual Machine Platform.
* Provides a hug array of chocie in terms of storage, memory, cpu and operating systems.
* By default the EBS root volume is deleted when the instance is terminated.
* Termination protected is turned off by default - Turn on to protect yourself from accidents!
* The user_data config field can contain bootstrapping code that is executed when your instance first boots up.
* [EC2 Pricing](https://aws.amazon.com/ec2/pricing/)
  * *On-Demand* - With On-Demand instances, you pay for compute capacity by the hour or the second depending on which instances you run. No longer-term commitments or upfront payments are needed. You can increase or decrease your compute capacity depending on the demands of your application and only pay the specified per hourly rates for the instance you use.
  * *Reserved* - You have a capacity reservation which offers significant discount compared to on-demand, but you are require to have a contact for 1–3 years. Used for applications with steady predictable use. However, you cant move between regions.
  * *Spot instances* - Amazon EC2 Spot instances allow you to request spare Amazon EC2 computing capacity for up to 90% off the On-Demand price.  Recommended for application that require very low compute prices, have flexible start and end times and can cope with being interruped.
** *Dedicated Hosts* - Exactly what is says - a dedicate hosts, used only by you. Can be good for situations involving restrictive software licenses, i.e. an Oracle server where specific CPUs must be licensed.
* [Security Groups](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html)
  * A virtual firewall for you EC2 Instances.
  * By default, all inbound traffic blocked, all outbound traffic allowed.
  * Stateful - if traffic is allowed in, outbound traffic for that request is allowed automatically.
  * You can attach more then one SG to an EC2 instance.
* [EC2 Hibernate](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Hibernate.html)
  * Put instance to sleep and return the to the same point when required.
  * Contents of RAM needs to be saved to the root EBS volume, so must have space to do this.
  * Works with General Purpose SSD (gp2 and gp3) and Provisioned IOPS SSD (io1 and io2).
  * Root EBS volume must be encrypted.
  * Useful for instances running services that take a long time to start up.
  * Any data on the instance store is lost when an instance is hibernated.
  * Can't hibernate > 60 days. Workaround -> start the instance again and re-hibernate.
* [EC2 Placement Groups](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html)
  * How EC2 instances are located on the underlying hardware.
    * Cluster - Place  instances in a single AZ. Good for low-latency network/HPC applications that require fast node-to-node connections.
    * Partition - Spread instances across logical partitions that do not share the same hardware as other partitions. Good for large distributed/replicated applications i.e. Cassandra, Hadoop and Kafka.
    * Spread - Spread a small group of instances across the underlying hardware.
    * There is no charge for creating a placement group.
    * 500 placement groups can be created in each region.
    * You cannot launch Dedicated Hosts in placement groups.
* [EC2 Instance Store](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html)
  * Temporary block-level storage for your instance.
  * Located on disks that are physically attached to the host computer.
  * Îdeal for temp storagem i.e. buffers, caches, scratch data, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.
  * Data is lost when...
    * The underlying disk drive fails.
    * The instance stops, hibernates or terminates.

#### [AWS Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/)

* Platform as a Service (PaaS).
* Useful for developers, i.e. stack-in-a-can.
* Pay only for underlying reosurces (EC2, ELB, ASG etc) not for Elastic Beanstalk itself.
* Recommended for development and testing purposes.
* Support multiple web frameworks/platforms...
  * Java/Tomcat.
  * PHP & Python/Apache HTTP.
  * Node.js/nginx.
  * .Net/Microsoft IIS.
  * Docker.
* Supports running multiple environments, i.e. dev, test, qa, staging etc.
* Supports versioning and allows for easy rollback.

#### [Amazon Elastic Container Service (Amazon ECS)](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html)

* Amazon's Docker offering - run, stop, start and manage containers on a cluster.
* Launch Types:
  * AWS Fargate - serverless, pay-as-you-go option.
    * Workloads - large workfload that must be optimize for low overhead, small workloads with occasional burst, tiny workloads, batch workloads.
  * AWS EC2 - Deploy EC2 Instances to run your containers.
    * Workloads - workloads requiring contant high cpu and mem usage, large workloads to be optimised for price, presistent storage requirement, compliance requires we manage our own infrastructure.

#### [Amazon Elastic Kubernetes Service (Amazon EKS)](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html)

* Manage Kubernetes Clusters on AWS.
* Runs and scale the Kubernetes control plan across multiple AZs.
* Scaling based on load and replaces unhealthy instances automatically.

#### Elastic Load Balancing

* [Amazon Elastic Load Balancing](https://aws.amazon.com/elasticloadbalancing/)
* Elastic Load Balancing (ELB) automatically distributes incoming application traffic across multiple targets and virtual appliances in one or more Availability Zones (AZs). 
* Support health checks to detect bad instances.
* Support TLS Termination.
* Exports useful metrics to CLoudwatch.
* Tip: If you expect a sudden huge spike in traffic you may want to ask AWS Support to [pre-warm your LB](https://aws.amazon.com/articles/best-practices-in-evaluating-elastic-load-balancing/#pre-warming)
* Cross Zone Load Balancing enables you to load balance across multiple AZ. Your load balancer nodes distribute incoming requests evenly across the Availability Zones enabled for your load balancer. Otherwise, each load balancer node distributes requests only to instances in its Availability Zone.
* [Application Load Balancer](https://aws.amazon.com/elasticloadbalancing/application-load-balancer/)
  * Operates at OSI Layer 7.
  * Best for HTTP and HTTPS applications.
  * Can intelligently route requests based on request content.
  * Path patterns allow yo to direct traffic to different EC2 instances based on the URL contained in the request.
  * Can route traffic to EC2 ASGs, Lambda, Fargate, EKS and ECS.
* [Network Load Balancer](https://aws.amazon.com/elasticloadbalancing/network-load-balancer/)
  * Operates at OSI Layer 4.
  * TCP & UDP Traffic.
  * Suited to High Performance used cases, can handle millions of requests per second.
* [Gateway Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/gateway/introduction.html)
* [Classic Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/introduction.html)
  * Operates at both OSI Layer 7 and 4.
  * Generally not as flexible as an ALB.

#### AWS Fargate

#### AWS Lambda

### Database

#### Amazon Aurora

#### Amazon DynamoDB

#### Amazon ElastiCache

#### Amazon RDS

#### Amazon Redshift

### Management and Governance

#### AWS Auto Scaling

* [Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html)
* Helps you ensure you always have the desired number of EC2 Instances for your application.
* Components of Amazon EC2 Auto Scaling
  * Groups - EC2 Instances organised into a group, we configure a minimum, desired and maximum number of instances,
  * Configuration Templates - Config for the EC2 instance AMI ID, instance type, key pair, security groups, ebs volume etc.
* [Scaling Options](https://docs.aws.amazon.com/autoscaling/ec2/userguide/scale-your-group.html#scaling-options) - We can scale up based on a schedule or in response to a specific condition (dynamic scaling) i.e. High CPU.
  * Maintain current instance levels at all times.
  * Scale manually.
  * Scale based on a schedule.
  * Scale based on demand.
  * Use predictive scaling - Uses machine learning and historical data from Cloudwatch to forcast scaling requirements.

#### [AWS Backup](https://aws.amazon.com/backup/)

* Centrally manage and automate backups across AWS Services.
* Supported Resources:
  * EC2
  * EBS Volumes
  * S3 Buckets
  * RDS Databases
  * Aurora Databases
  * DynamoDB Tables
  * Netptune Databases
  * EFS
  * FSx file systems
  * Storage Gateway Volumes
  * VMWare workloads

#### [AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)

* Infrstructure as code - model and provising infrastructure in a single text file.
* YAML or JSON.
* Cloudformation Components:
  * Resources - Define EC2 Instances, LBS, VPCs, Subnets etc.
  * Parameters - Define runtime input parameters.
  * Mappings - Static variables in the template.
  * Outputs - Define variables to return once a stack is created, i.e. an ELB DNS Name.
  * Conditionals - Define under what circumstances to perform an action.
  * Metadata.
  * Template helpders: References and Functions.
* Use case:
  * Setup the same resources for dev, test, uat, staging etc.
  * Developer stacks.
  * Reference architecture.

#### [AWS CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)

* Provides and auto/event history of all the actions taken by a user, whether in web console, cli or sdk.
* Enabled by default in all regions.
* Cloudtrail logs can be sent to CLoudWatch logs or an S3 Bucket,
* Use: Who deleted what and when?

#### [Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)

* Collect metrics, monitor log files, set alarms for AWS Resources, i.e. EC2, ALB, S3, Lambda, RDS etc.
* By default metrics are logged a 1 minute intervals, can be set to a max of 1 second.
* Cloudwatch Logs Agent needs to be [installed on EC2](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/install-CloudWatch-Agent-on-EC2-Instance.html).
* CLoudwatch can be accessed via:
  * [CLoudwatch Console](https://console.aws.amazon.com/cloudwatch/)
  * AWS CLI
  * [Cloudwatch API](http://docs.aws.amazon.com/AmazonCloudWatch/latest/APIReference/Welcome.html)
  * AWS SDKs

#### [AWS Config](https://aws.amazon.com/config/)

* Record and assess configuration of AWS Resources.
* Notify via SNS for any configuration change.
* Integrated with CloudTrail.
* Use Cases
  * PCI-DSS or HIPAA STandard Compliance.
  * Troubleshooting - what config changes have happened recently?
  * Security Analysis - continually monitor your resources for security weaknesses. 

#### [Amazon EventBridge (Amazon CloudWatch Events)](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)

* Serverless event bus service.
* Connect applications with data streams from various sources.
* Eventbridge has the concepts of...
  * Events - a change in an AWS Service or other application.
  * Event Source
  * Event buses - a pipeline that receives events.
  * Rules - apply conditions to events.
  * Targets - a resource or endpoint to send the event to (can define up to 5 targets for each rule).
* Use Cases:
  * Simple cron-tye events, i.e. run logrotate when disk space is >90% full.
  * Event-driven architectures.
* [Amazon EventBridge Overview](https://medium.com/awesome-cloud/aws-amazon-eventbridge-overview-what-is-aws-eventbridge-eventbus-introduction-features-use-cases-benefits-41c05f411317)

#### [AWS Organizations](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_introduction.html)

* Centralized management of all of your AWS accounts.
* Consolidated billing for all member accounts.
* Hierarchical grouping of your accounts to meet your budgetary, security, or compliance needs.
* Centralize control over the AWS services and API actions that each account can access.
* Standardize tags across the resources in your organization's accounts.
* Control how AWS artificial intelligence (AI) and machine learning services can collect and store data.
* Configure automatic backups for the resources in your organization's accounts.
* IAM (Identity & Access Management) Support.
* Free to use.

#### [AWS Resource Access Manager](https://docs.aws.amazon.com/ram/latest/userguide/what-is.html)

* Shares resource with other AWS Accounts.
* Use Cases:
  * Create a resource once and share it via AWS RAM - Remove need for duplication of resources.
* Supported Resource Types:
  * EC2
  * Aurora
  * Route 53
  * App Mesh
  * Outposts

#### [AWS Systems Manager](https://aws.amazon.com/systems-manager/)

* Operations/Management Hub for your AWS applications.
* Contains many tools and services
  * [Explorer](https://aws.amazon.com/systems-manager/features/#Explorer) View your AWS Environment.
  * [Parameter Store](https://aws.amazon.com/systems-manager/features/#Parameter_Store) - Centralized store for configuration data, i.e. db connection strings.
  * [Change Manager](https://aws.amazon.com/systems-manager/features/#Change_Manager) - Organise and manage system changes.
  * [Automation](https://aws.amazon.com/systems-manager/features/#Automation) - Automate common tasks.
  * [Maintenance Windows](https://aws.amazon.com/systems-manager/features/#Maintenance_Windows) - Define and manage maintenance windows to perform tasks across instances.
  * [Patch Manager](https://aws.amazon.com/systems-manager/features/#Patch_Manager) - Manage the rollout of Operating System patches.
  * [Many More](https://aws.amazon.com/systems-manager/features/)

#### AWS Trusted Advisor

### Migration and Transfer

#### AWS Database Migration Service (AWS DMS)

#### AWS DataSync

#### AWS Migration Hub

#### AWS Server Migration Service (AWS SMS)

#### AWS Snowball

#### AWS Transfer Family

### Networking and Content Delivery

#### Amazon API Gateway

#### [Amazon CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)

* Content Delivery Network (CDN) - AWS edge location to cache and deliver content.
* Global Service.
* Can cache data from S3 Buckets, EC2 or ELB.
* Two types:
  * Web Distributions which are used for websites.
  * RTMP Distributions which are used for streaming media.
* Objects are cahced for the TTL.
* Can generate a signed url or signed cookie for file, i.e. premium services.
* Integrates with AWS WAF (Web Application Firewall).

#### [AWS Direct Connect](https://aws.amazon.com/directconnect/)

* Dedicated private connection from on-prem to AWS VPC Network.
* 1GB to 100GB/s network bandwidth.
* Can take day or weeks to organise.

#### [AWS Global Accelerator](https://docs.aws.amazon.com/global-accelerator/latest/dg/what-is-global-accelerator.html)

* improve the performance of your application for local and global users.
* Standard Accelerator - directs traffic, over the AWS Global Network, to endpoints in the nearest region to the client.
* Custom Routing Accelerator - maps one or more users to a specific destination.

#### [Amazon Route 53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html)

* Amazon Route 53 is a highly available and scalable Domain Name System (DNS) web service. 
* Use Cases
  * Register domain names.
  * Route internet traffic to the resources for your domain.
  * Check the health of your resources.

#### [AWS Transit Gateway](https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html)

* Network transit hub - connect VPCs and on-premises network together.
* Data is encrypted and never travels over the public internet.
* Hub and spoke(star) connection.
* Supports IP [Multicast](https://docs.aws.amazon.com/vpc/latest/tgw/tgw-multicast-overview.html).
* Can be connected to: VPCs, AWS Direct COnnection Gateways, VPNC Connections, as well as other Transit Gateways. 

#### Amazon VPC (and associated features)

### Security, Identity, and Compliance

#### AWS Certificate Manager (ACM)

#### AWS Directory Service

#### Amazon GuardDuty

* Read VPC Flow Logs, DNS Logs, and CloudTrail events.
* Apply ML algorithms and anomaly detections to discover threats.

#### AWS Identity and Access Management (IAM)

#### Amazon Inspector

#### AWS Key Management Service (AWS KMS)

#### [Amazon Macie](https://aws.amazon.com/macie/)

* Amazon Macie is a fully managed data security and data privacy service that uses machine learning and pattern matching to discover and protect your sensitive data in AWS.
* Macie automatically provides an inventory of Amazon S3 buckets including a list of unencrypted buckets, publicly accessible buckets, and buckets shared with AWS accounts outside those you have defined in AWS Organizations. Then, Macie applies machine learning and pattern matching techniques to the buckets you select to identify and alert you to sensitive data, such as personally identifiable information (PII).
* Use cases
  * Assessing your data privacy and security
  * Maintaining regulatory compliance
  * Identifying sensitive data in data migrations

#### [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/)

* Protect and manage secrets needed by your applications and services.
* Rotate Amazon RDS, Redhsift and DocumentDB credentials automatically.
* Fine-grained paccess policies with IAM.
* Replicate secrets across regions.
* [Pricing](https://aws.amazon.com/secrets-manager/pricing/)
  * $0.40 per secret, per month.
  * $0.05 per 10K API calls.

#### [AWS Shield](https://aws.amazon.com/shield/)

* Managed DDoS protection.
* Protect against layer 3 & 4 attacks (Network and Transport).
* 2 Offerings
  * Standard - automatic and free DDoS protection service for all AWS customers for CloudFront and Route 53 resources.
  * Advanced - paid service for enhanced DDoS protection for EC2, ELB, CloudFront, and Route 53 resources

#### AWS Single Sign-On

#### [AWS WAF](https://aws.amazon.com/waf/)

* Web Application Firewall.
* Proects your wbe app or api against common web exploits.
* Create rules that can block common attacks, i.e. SQL injection or cross-site scripting (Layer 7,application).
* Monitor http & https requests sent to Cloudfront,, LBs or API Gateway.
* WAF Conditions - what we might want to allow or block requests on.
  * Request header values.
  * Country of request origin.
  * IP Address.
  * Strings that appear in requests.
  * Request length.
  * Presence of SQL code.
  * Presence of a script.
* Pay for what you use - based on number of rules & requests.
* You can deploy WAF on CloudFront, Application Load Balancer, API Gateway and AWS AppSync

### Storage

#### Amazon Elastic Block Store (Amazon EBS)

* [Amazon EBS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html)
* Block level storage volumes for use with EC2 instances.
* Automatically replicated with an AZ.
* Volumes can only be mounted to instances within the same AZ.
* Snapshots - point in time copies, stores in S3, can be restored in new regions, snapshots are incremental.
* When snapshotting root device — best practice to terminate it first (Ensure volumes is not set to be destroyed with instance).
* If a volume is encrypted then the snapshots are encrypted too.
* Volume Types
  * General Purpose SSD volumes (gp2 and gp3
    * Balanced price and performance.
    * Ideal for boot volumes, medium sized single-instance dbs, dev and test instances.
  * Provisioned IOPS SSD volumes (io1 and io2)
    *  I/O-intensive workloads.
    * IOPS rate specified when creating the volume.
  * Throughput Optimized HDD volumes (st1)
    * Low-cost magnetic storage that defines performance in terms of throughput rather than IOPS.
    * Ideal for large, sequential workloads such as Amazon EMR, ETL, data warehouses, and log processing.
  * Cold HDD volumes (sc1)
    * Low-cost magnetic storage that defines performance in terms of throughput rather than IOPS.
    * These volumes are ideal for large, sequential, cold-data workloads.
* Performance metrics, such as bandwidth, throughput, latency, and average queue length, are available through the AWS Management.

#### Amazon Elastic File System (Amazon EFS)

* [Amazon EFS](https://aws.amazon.com/efs/)
* Managed NFS version 4 (NFSv4).
* Can be mounted on an EC2 instance.
* Data stored acorss multiple AZs.
* Native to Unix & Linux, but not supported on Windows instances.

#### [Amazon FSx](https://aws.amazon.com/fsx/)

* Choice of 4 widely-used file systems:
  * Netapp ONTAP - run workloads based on NFS/SMB/iSCSI.
  * OpenZFS - run workloads on Linux, machine learning or application iwth high-IOPS storage requirements. Clone application data in seconds with ZFS SNapshots.
  * Windows File Server - Use for Windows Application, i.e. Sharepoint.
  * Lustre - Use for high performance computing, machine learning and big data analytics.

#### [Amazon S3](https://aws.amazon.com/s3/?nc1=h_ls)

#### [Amazon S3 Glacier](https://docs.aws.amazon.com/amazonglacier/latest/dev/introduction.html)

#### [AWS Storage Gateway](https://aws.amazon.com/storagegateway/)

* Enable on-premise access to almost unlimited cloud storage.

# Further Reading / References

* [OSI Model - Wikipedia](https://en.wikipedia.org/wiki/OSI_model)
* [What is the OSI Model](https://www.imperva.com/learn/application-security/osi-model/)
* [ELB vs. ALB vs. NLB: Choosing the Best AWS Load Balancer for Your Needs](https://iamondemand.com/blog/elb-vs-alb-vs-nlb-choosing-the-best-aws-load-balancer-for-your-needs/)
* [Routing traffic to an ELB load balancer](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-to-elb-load-balancer.html)
* [AWS SSA Exam Notes](https://codingnconcepts.com/aws/aws-saa-exam-notes)
* [AWS Solution Architect Associate Exam Study Notes](https://chloemcateer.medium.com/aws-solution-architect-associate-exam-study-notes-b6c5884ee500)