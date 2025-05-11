# Content

- [Serverless Services](#serverless-services)
- [Databases](#databases)
- [EC2]
- [VPC](#vpc)
- [Security Group](#security-group)
- [AWS Systems Manager](#aws-systems-manager)

# Serverless Services

- DynamoDB

# Databases

### DynamoDB

- Fully Managed, Serverless
- NoSQL (schemaless, key-value db)
- Continuous backups, Automated multi-region replication (offers active-active cross-region support)
- **DynamoDB Global Tables**: replicate data automatically across regions and scale capacity to handle workloads.
- **DynamoDB Accelerator (DAX)**: in-memory cache

### Aurora

- Fully managed RDS (MySQL and PostgreSQL)
- Higher throughput and faster performance than normal RDS.
- Supports multi-master (all instances can read/write).

### RDS (Relational Database Server)

- Resizable capacity
- Automates hardware provisioning, database setup, patching and backups.
- Supports MySQL, PostgreSQL

# EC2 (Elastic Compute Cloud)

- Charged per second, minimum charge is 60 seconds.

# VPC

### NAT Gateway

- Enable instances in **private subnet** to **connect to internet or other AWS services**
- Prevents internet from connecting to instances in private subnet
- Associate Elastic IP to NAT Gateway
- NAT Gateway managed by AWS, NAT Instance managed by you.

### Network ACL (Access Control List)

- Firewall for VPC **subnet** to control inbound and outbound traffic
- Can **ALLOW or DENY** traffic.
- **Stateless**: responses that allowed inbound traffic are subject to rules for outbound traffic (vice versa)

# Security Group

- Virtual firewall for your instance to control inbound and outbound traffic.
- Can specify **ALLOW** rules only.
- **Stateful**: If you allow traffic in one direction, the return traffic is automatically allowed, regardless of the rules.

# AWS Systems Manager

- Provides user interface to view **operational data** from multiple AWS services.
- Automates operational tasks
  1. Apply patches to EC2 or on-premises instances
  2. Run commands
  3. Configure servers across AWS or on-premises
