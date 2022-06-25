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
#### Amazon Athena
#### Amazon Elasticsearch Service (Amazon ES)
#### Amazon EMR
#### AWS Glue
#### Amazon Kinesis
#### Amazon QuickSight
### AWS Billing and Cost Management:
#### AWS Budgets
#### Cost Explorer
### Application Integration:
#### Amazon Simple Notification Service (Amazon SNS)
#### Amazon Simple Queue Service (Amazon SQS)
### Compute
#### Amazon EC2
* Amazon's Virtual Machine Platform.
* Provides a hug array of chocie in terms of storage, memory, cpu and operating systems.
* By default the EBS root volume is deleted when the instance is terminated.
* Termination protected is turned off by default - Turn on to protect yourself from accidents!
* The user_data config field can contain bootstrapping code that is executed when your instance first boots up.
* [EC2 Pricing](https://aws.amazon.com/ec2/pricing/)
** *On-Demand* - With On-Demand instances, you pay for compute capacity by the hour or the second depending on which instances you run. No longer-term commitments or upfront payments are needed. You can increase or decrease your compute capacity depending on the demands of your application and only pay the specified per hourly rates for the instance you use.
** *Reserved* - You have a capacity reservation which offers significant discount compared to on-demand, but you are require to have a contact for 1–3 years. Used for applications with steady predictable use. However, you cant move between regions.
** *Spot instances* - Amazon EC2 Spot instances allow you to request spare Amazon EC2 computing capacity for up to 90% off the On-Demand price.  Recommended for application that require very low compute prices, have flexible start and end times and can cope with being interruped.
** *Dedicated Hosts* - Exactly what is says - a dedicate hosts, used only by you. Can be good for situations involving restrictive software licenses, i.e. an Oracle server where specific CPUs must be licensed.
* [Security Groups](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html)
** A virtual firewall for you EC2 Instances.
** By default, all inbound traffic blocked, all outbound traffic allowed.
** Stateful - if traffic is allowed in, outbound traffic for that request is allowed automatically.
** You can attach more then one SG to an EC2 instance.
* [EC2 Hibernate](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Hibernate.html)
** Put instance to sleep and return the to the same point when required.
** Contents of RAM needs to be saved to the root EBS volume, so must have space to do this.
** Works with General Purpose SSD (gp2 and gp3) and Provisioned IOPS SSD (io1 and io2).
** Root EBS volume must be encrypted.
** Useful for instances running services that take a long time to start up.
** Any data on the instance store is lost when an instance is hibernated.
** Can't hibernate > 60 days. Workaround -> start the instance again and re-hibernate.
* [EC2 Placement Groups](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html)
** How EC2 instances are located on the underlying hardware.
*** Cluster - Place  instances in a single AZ. Good for low-latency network/HPC applications that require fast node-to-node connections.
*** Partition - Spread instances across logical partitions that do not share the same hardware as other partitions. Good for large distributed/replicated applications i.e. Cassandra, Hadoop and Kafka.
*** Spread - Spread a small group of instances across the underlying hardware.
*** There is no charge for creating a placement group.
*** 500 placement groups can be created in each region.
*** You cannot launch Dedicated Hosts in placement groups.

#### AWS Elastic Beanstalk
#### Amazon Elastic Container Service (Amazon ECS)
#### Amazon Elastic Kubernetes Service (Amazon EKS)
#### Elastic Load Balancing
* [Amazon Elastic Load Balancing](https://aws.amazon.com/elasticloadbalancing/)
* Elastic Load Balancing (ELB) automatically distributes incoming application traffic across multiple targets and virtual appliances in one or more Availability Zones (AZs). 
* Support health checks to detect bad instances.
* Support TLS Termination.
* Exports useful metrics to CLoudwatch.
* Tip: If you expect a sudden huge spike in traffic you may want to ask AWS Support to [pre-warm your LB](https://aws.amazon.com/articles/best-practices-in-evaluating-elastic-load-balancing/#pre-warming)
* Cross Zone Load Balancing enables you to load balance across multiple AZ. Your load balancer nodes distribute incoming requests evenly across the Availability Zones enabled for your load balancer. Otherwise, each load balancer node distributes requests only to instances in its Availability Zone.
* Application Load Balancer
  * Operates at OSI Layer 7.
  * Best for HTTP and HTTPS applications.
  * Can intelligently route requests based on request content.
  * Path patterns allow yo to direct traffic to different EC2 instances based on the URL contained in the request.
  * Can route traffic to EC2 ASGs, Lambda, Fargate, EKS and ECS.
* Network Load Balancer
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
#### AWS Backup
#### AWS CloudFormation
#### AWS CloudTrail
#### Amazon CloudWatch
#### AWS Config
#### Amazon EventBridge (Amazon CloudWatch Events)
#### AWS Organizations
#### AWS Resource Access Manager
#### AWS Systems Manager
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
#### Amazon CloudFront
#### AWS Direct Connect
#### AWS Global Accelerator
#### [Amazon Route 53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html)
* Amazon Route 53 is a highly available and scalable Domain Name System (DNS) web service. 
* Use Cases
  * Register domain names.
  * Route internet traffic to the resources for your domain.
  * Check the health of your resources.
#### AWS Transit Gateway
#### Amazon VPC (and associated features)
### Security, Identity, and Compliance:
#### AWS Certificate Manager (ACM)
#### AWS Directory Service
#### Amazon GuardDuty
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

#### AWS Secrets Manager
#### AWS Shield
#### AWS Single Sign-On
#### AWS WAF
### Storage
#### Amazon Elastic Block Store (Amazon EBS)
#### Amazon Elastic File System (Amazon EFS)
#### Amazon FSx
#### Amazon S3
#### Amazon S3 Glacier
#### AWS Storage Gateway

# Further Reading

* [OSI Model - Wikipedia](https://en.wikipedia.org/wiki/OSI_model)
* [What is the OSI Model](https://www.imperva.com/learn/application-security/osi-model/)
* [ELB vs. ALB vs. NLB: Choosing the Best AWS Load Balancer for Your Needs](https://iamondemand.com/blog/elb-vs-alb-vs-nlb-choosing-the-best-aws-load-balancer-for-your-needs/)
* [Routing traffic to an ELB load balancer](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-to-elb-load-balancer.html)