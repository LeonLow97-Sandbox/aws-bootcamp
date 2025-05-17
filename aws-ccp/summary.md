# IAM

- **Users**: mapped to a physical user, has a password for AWS Console
- **Groups**: contains users only
- **Policies**: JSON document that outlines permissions for users or groups
- **Roles**: for EC2 instances or AWS services
- **Security**: MFA + Password policy
- **AWS CLI**: manage your AWS services using the command-line
- **AWS SDK**: manage you AWS services using a programming language
- **Access Keys**: access AWS using the CLI or SDK
- **Audit**: IAM Credentials Report and IAM Access Advisor

# EC2

- **EC2 Instance**: AMI (OS) + Instance Size (CPU + RAM) + Storage + Security Groups + EC2 User Data (bootstrap script)
- **Security Groups**: Firewall attached to the EC2 instance (filter by ports and IP)
- **EC2 User Data**: Script launched at the first start of an instance
- **SSH**: start a terminal into our EC2 Instances (port 22)
- **EC2 Instance Role**: link to IAM roles
- **Purchasing Options**: On-Demand, Spot, Reserved (Standard + Convertible), Dedicated Host, Dedicated Instance, Savings Plan

# EC2 Instance Storage

- **EBS Volumes**:
  - network drives attached to 1 EC2 instance at a time
  - tied to an AZ
  - can use EBS snapshots for backups / transferring EBS volumes across AZ
- **AMI**: create ready-to-use EC2 instances with our customizations
- **EC2 Image Builder**: automatically build, test and distribute AMIs
- **EC2 Instance Store**:
  - High performance hardware disk attached to our EC2 instance
  - Lost if our instance is stopped / terminated
- **EFS**: network file system, can be attached to 100s of instances in a region
- **EFS-IA**: cost-optimized storage class for infrequent accessed files
- **FSx for Windows**: network file system for Windows servers
- **FSx for Lustre**: high performance computing (HPC) Linux file system

# ELB & ASG Summary

- **Elastic Load Balancer (ELB)**:
  - distribute traffic across EC2 instances, can be multi-AZ
  - supports health checks
  - 4 types: Classic (old), Application (HTTP - L7), Network (TCP - L4), Gateway (L3)
- **Auto Scaling Groups (ASG)**:
  - implement elasticity for your application, across multiple AZ
  - scale EC2 instances based on the demand on your system, replace unhealthy
  - integrated with ELB

# S3 (Simple Storage Service)

- **Buckets vs Objects**: global unique name, tied to a region
- **S3 Security**: IAM policy, S3 Bucket Policy (Public Access), S3 Encryption
- **S3 Websites**: host a static website on S3 (allow public access)
- **S3 Versioning**: multiple versions of files, prevent accidental deletion (enables rollback)
- **S3 Replication**: same-region or cross-region, must enable versioning
  - **SRR**: backup, compliance and disaster recovery
  - **CRR**: improved performance, data redundancy, compliance and disaster recovery
- **S3 Storage Classes**: Standard IA, One Zone-IA, Intelligent, Glacier (Instant, Flexible, Deep)
- **Snow Family**: import data onto S3 through a physical device, edge computing
  - Snowcone: small, portable device (8TB storage)
  - Snowball: rugged, portable device (50 - 80TB storage), used for bulk data transfer to S3
  - Snowmobile: 40-foot shipping container (up to 100 PB of storage), extremely large-scale data transfer to S3, data center migrations or large-scale disaster recovery
- **OpsHub**: desktop application to manage Snow Family devices
- **Storage Gateway**: hybrid solution to extend on-premises storage to S3

# Databases & Analytics

- **Relational Databases - OLTP**: RDS & Aurora (SQL)
- **Differences between Multi-AZ, Multi-Region, Read Replicas**
  - Multi-AZ: Availability
  - Multi-Region: Disaster recovery and local performance
  - Read Replicas: Scalability
- **In-Memory Database**: ElastiCache
- **Key/Value Database**: DynamoDB (serverless) & DAX (cache for DynamoDB)
- **DocumentDB**: "Aurora for MongoDB" (JSON - NoSQL database)
- **Warehouse - OLAP**: Redshift (SQL)
- **Hadoop Cluster**: EMR
- **Athena**: query data on S3 (serverless and SQL)
- **QuickSight**: dashboards on your data (serverless)
- **AWS QLDB**: Financial Transactions Ledger (immutable journal, cryptographically verifiable), centralized db
- **AWS Managed Blockchain**: managed Hyperledger Fabric & Ethereum blockchains, decentralized db
- **Glue**: Managed ETL and Data Catalog service (to discover datasets)
- **Database Migration**: DMS
- **Neptune**: graph database
- **Timestream**: time-series database

# Other Compute

- **AWS ECS**: run Docker containers on EC2 instances (you provision EC2 instances in advance)
- **AWS Fargate**:
  - Run docker containers without provisioning the infrastructure
  - Serverless (no EC2 instances)
- **ECR**: private docker images repository
- **Batch**: run batch jobs on AWS across managed EC2 instances (batch runs on top of ECS service)
- **Lightsail**: (for cloud beginners) predictable & low pricing for simple application and DB stacks
- **Lambda**:
  - serverless, Function as a Service, seamless scaling, reactive
  - supports many programming languages except (arbitrary) Docker
  - invocation time is up to 15 minutes
- **Lambda Billing**:
  - computation time
  - number of requests
- **Lambda Use Cases**:
  - create thumbnails for images uploaded onto S3
  - run a serverless cron job
- **API Gateway**: expose Lambda functions as HTTP API

# Deployment

- **CloudFormation (AWS)**:
  - Infrastructure as Code, works with almost all of AWS resources
  - Repeat across Regions and Accounts using CloudFormation Templates
  - JSON or YAML
- **Beanstalk (AWS)**:
  - Platform as a Service (PaaS), limited to certain programming languages or Docker
  - Deploy code consistently with a known architecture: ALB + EC2 + RDS
- **Systems Manger (hybrid)**:
  - patch, configure and run commands at scale
  - gives visibility and control of your AWS infrastructure
- **CodeDeploy (hybrid)**: deploy and upgrade any application onto servers
- **CodeCommit**: deprecated, store code in private git repository (version control)
- **CodeBuild**: Build and test code in AWS, serverless
- **CodePipeline**: Orchestration of pipeline (from code to build to deploy)
- **CodeArtifact**: Store software packages / dependencies on AWS
- **AWS CDK**: define your cloud infrastructure using a programming language, translates to CloudFormation

# Global Applications

- **Route 53**:
  - great to route users to the closest deployment with least latency
  - great for disaster recovery strategies
  - DNS, health checks, routing policies
- **CloudFront**:
  - replicate part of your application to AWS Edge Locations: decrease latency
  - Cache common requests: improved user experience and decrease latency
  - security: shield and WAF
- **S3 Transfer Acceleration**:
  - accelerate global uploads and downloads into S3
  - routes data through edge location, then to S3 bucket, faster data transfer
- **AWS Global Accelerator**: improve global application availability and performance using the AWS global network via edge locations. for global clients to access app endpoints (e.g., EC2, ALB. NLB)
- **AWS Outposts**: deploy outposts racks in your own data centers to extend AWS services
- **AWS Wavelength**:
  - brings AWS services to the edge of 5G networks
  - ultra-low latency applications
- **AWS Local Zones**:
  - brings AWS resources (compute, database, storage) closer to your users
  - good for latency-sensitive applications

# Integration

- **SQS**:
  - Queue service in AWS
  - Multiple Producers, messages are kept up to 14 days
  - Multiple Consumers share the read and delete messages when done
  - Used to **decouple** applications in AWS
- **SNS**:
  - Notification service in AWS
  - Subscribers: Email, Lambda, SQS, HTTP, Mobile
  - Multiple Subscribers, send messages to all of them
  - No message retention
- **Kinesis**: real-time data streaming, persistence and analysis
- **AWS MQ**:
  - managed message broker for ActiveMQ and RabbitMQ in the cloud (MQTT, AMQP protocols)
  - for migrating existing messaging systems to AWS without changing much code

# Monitoring

- **CloudWatch**
  - **Metrics**: monitor the performance of AWS services and billing metrics
  - **Alarms**: automate notification, perform EC2 action, notify to SNS based on metric
  - **Logs**: collect log files from EC2 instances, servers, Lambda functions
  - **Events (or EventBridge)**: react to events in AWS, or trigger a rule on a schedule
- **CloudTrail**: audit API calls made within your AWS account, e.g., check who deleted an AWS resource
- **CloudTrail Insights**: automated analysis of your CloudTrail Events
- **X-Ray**: trace requests made through your distributed applications / microservices
- **AWS Health Dashboard**: status of all AWS services across all regions
- **AWS Account Health Dashboard**: AWS events that impact YOUR infrastructure
- **AWS CodeGuru**: automated code reviews and application performance recommendations

# VPC

- **Subnets**: Tied to an AZ, network partition of VPC
- **Internet Gateway**: at the VPC level, provide internet access
- **NAT Gateway / Instances**: give internet access to private subnets
- **NACL**: stateless, subnet rules for inbound and outbound, ALLOW and DENY rules
- **Security Groups**: stateful, operate at the EC2 instance level, ALLOW rule only
- **VPC Peering**: connect 2 VPCs with non-overlapping IP ranges, non-transitive
- **Elastic IP**: fixed public IPv4, ongoing cost if not in use
- **VPC Endpoint**: provide private access to AWS services within VPC
- **Site-to-Site VPN**: VPN over public internet between on-premises DC and AWS
  - **PrivateLink**: privately connect to a service in a 3rd party VPC
  - Customer: Customer Gateway
  - AWS: Virtual Private Gateway
- **Client VPN**: OpenVPN connection from your computer into your VPC
- **Direct Connect**: direct private connection to AWS
- **Transit Gateway**: connect thousands of VPC and on-premises networks together
- **AWS VPN**: connect on-premises to AWS over public internet using encrypted VPN tunnels.

# Security & Compliance

- **AWS Shield**: Automatic DDoS Protection + 24/7 support for advanced
- **WAF**: Firewall to filter incoming requests based on rules
- **KMS**: Encryption keys managed by AWS
- **CloudHSM**: Hardware encryption, we manage encryption keys
- **AWS Certificate Manager**: provision, manage and deploy SSL/TLS certificates
- **Artifact**: Get access to compliance reports such as PCI/ISO, etc ...
- **GuardDuty**: find malicious behavior with VPC, DNS & CloudTrail Logs
- **Inspector**: find software vulnerabilities in EC2, ECR Images and Lambda functions
- **Network Firewall**: protect VPC against network attacks 💚
- **Config**: track config changes and compliance against rules
- **Macie**: find sensitive data (e.g., PII data) in S3 buckets.
- **CloudTrail**: track API calls made by users within account
- **AWS Security Hub**: gather security findings from multiple AWS accounts 💚
- **AWS Detective**: find the root cause of security issues or suspicious activities 💚
- **AWS Abuse**: report AWS resources used for abusive or illegal purposes
- **Root User Privileges**:
  - Change account settings
  - Close your AWS account
  - Change or cancel your AWS Support Plan
  - Register as a seller in the Reserved Instance Marketplace
- **IAM Access Analyzer**: identify which resources are shared externally (outside Zone of Trust) 💚
- **Firewall Manager**: manage security rules across an Organization (WAF, Shield, ...) 💚

# Machine Learning

- **Rekognition**: face detection, labeling, celebrity recognition
- **Transcribe**: audio to text (e.g., subtitles)
- **Polly**: text to audio
- **Translate**: language translations
- **Lex**: build conversational bots - chatbots
- **Connect**: cloud contact center
- **Comprehend**: natural language processing
- **SageMaker**: machine learning for every developer and data scientist, build ML models
- **Forecast**: build highly accurate forecasts
- **Kendra**: ML-powered search engine, document search service 💚
- **Personalize**: real-time personalized recommendations
- **Textract**: detect text and data in documents 💚

# Account Best Practices

- Operate multiple accounts using **Organizations**
- Use **SCP (service control policies)** to restrict account power
- Easily setup multiple accounts with best practices with **AWS Control Tower**, sits on top of Organization
- **Use Tags and Cost Allocation Tags** for easy management and billing
- **IAM guidelines**: MFA, least-privilege, password policy, password rotation
- **Config** to record all resources configurations and compliance over time
- **CloudFormation**: to deploy stacks across accounts and regions
- **Trusted Advisor** to get insights, Support Plan adapted to your needs
- Send Service Logs and Access Logs to **S3 or CloudWatch Logs**
- **CloudTrail** to record API calls made within your account
- **If your account is compromised**, change the root password, delete and rotate all passwords / keys, contact AWS support
- Allow users to create pre-defined stacks defined by admins using **AWS Service Catalog**

# Billing and Costing Tools

- **Compute Optimizer**: recommends resources' configurations to reduce cost
- **Pricing Calculator**: calculate cost of services on AWS
- **Billing Dashboard**: high level overview + free tier dashboard 💚
- **Cost Allocation Tags**: tag resources to create detailed reports, can use tags as filter
- **Cost and Usage Reports**: most comprehensive billing dataset
- **Cost Explorer**: view current and historical usage (detailed) and forecast usage
- **Billing Alarms**: stored in us-east-1, track overall and per-service billing
- **Budgets**: more advanced - track usage, costs, RI and get alerts
- **Savings Plans**: easy way to save based on long-term usage of AWS
- **Cost Anomaly Detection**: detect unusual spends using ML 💚
- **Service Quotas**: notify you when you are close to service quota threshold

# Advanced Identity

- **IAM**
  - Identity and Access Management inside your AWS account
  - For users that you trust and belong to your company
- **Organizations**: manage multiple accounts
- **Security Token Service (STS)**: temporary, limited-privileges credentials to access AWS resources.
- **Cognito**: create a database of users for your mobile and web applications
- **Directory Services**: integrate Microsoft Active Directory in AWS
- **IAM Identity Center**: one login for multiple AWS accounts and applications

# Other Services 💚

- **AWS WorkSpaces**: managed Desktop as a Service to provision Windows or Linux desktops, eliminate on-premise VDI (Virtual Desktop Infrastructure)
  - full, personalized desktop
- **AWS AppStream 2.0**: desktop application streaming service, delivered from web browser, no need VDI
  - runs apps via browser, in a stateless, scalable way
- **AWS IoT Core**: connect IoT devices to AWS, serverless
- **AWS Elastic Transcoder**: convert media files stored in S3 to media files in formats required by consumer playback devices (e.g., phones).
- **AWS AppSync**: make use of `GraphQL`. store and sync data across mobile and web apps in real time.
- **AWS Amplify**: tools to develop and deploy full stack web and mobile apps
- **AWS Application Composer**: visually build serverless apps, generates IaC using CloudFormation
- **AWS Device Farm**: managed service that test your web and mobile apps against desktop browsers, mobile devices and tablets
- **AWS Backup**: managed service to centrally manage and automate backups across AWS services
- **AWS DataSync**: move large amount of data from on-premises to AWS, replication tasks are incremental after first full load
- **Cloud Migration Strategies** (7 Rs):
  - Retire, Retain, Relocate, Rehost (lift and shift), Replatform (lift and reshape), Repurchase (drop and shop), Refactor/Re-architect
- **AWS Application Discovery Service**: plan migration projects by gathering info about on-premises data centers. Agentless discovery and agent-based discovery
- **AWS Application Migration Service (MGN)**: rehost (list and shift) solution, simplifies **migrating** apps to AWS
- **AWS Migration Evaluator**: build data-driven business case for migration to AWS
- **AWS Migration Hub**: central location to collect servers and apps inventory data for migrations to AWS
  - AWS Migration Hub Orchestrator
  - supports migration status updates from MGN and DMS
- **AWS Fault Injection Simulator (FIS)**: managed service for running fault injection on AWS workloads, based on **chaos engineering**
- **AWS Step Functions**: serverless visual workflow to orchestrate Lambda functions
- **AWS Ground Station**: managed service to control _satellite_ communications
- **AWS Pinpoint**: 2-way (outbound/inbound) marketing communications service, personalize messages with right content to customers
