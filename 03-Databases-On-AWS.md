# What is a relational database?
* Think of a traditional spreadsheet:
    - Database
    - Tables
    - Rows
    - Columns (Fields)
* RDS runs on virtual machines.
* You cannot log in to these operating systems.
* Patching of the RDS Operating System and DB is Amazon's responsibility.
* RDS is not serverless, however Aurora Serverless is serverless.
* There are two different types of backups for RDS:
    - Automated Backups
    - Database snapshots
* I/O may be briefly suspended while the backup process initializes (typically under a few seconds), and you may experience a brief period of elevated latency.
* Amazon RDS with provisioned IOPS delivers fast, predictable, and consistent I/O performance that is great for OLTP database workloads.

# Types of Relational Databases on AWS
* SQL Server
* Oracle
* MySQL Server
* PostgreSQL
* Aurora
* MariaDB

# Non-Relational Databases
* Collection = Table
* DynamoDB (No SQL)
* Document = Row
* Key Value Pairs = Columns (Fields)
* JSON format

# Multi-AZ vs Read Replicas
* RDS has two key features:
    - Multi-AZ - For Disaster Recovery
    - Read Replicas - For Performance (Up to 5 copies)

## Read Replicas
* Can be Multi-AZ.
* Used to increase performance.
* Must have backups turned on.
* Can be in different regions.
* Can be MSSQL, MySQL, PostgreSQL, MariaDB, Oracle, Aurora.
* Can be promoted to master but this will break the Read Replica.

## Multi- AZ
* Used for Disaster Recovery
* You can force a failover from one Availability Zone to another by rebooting the RDS instance.

# Encryption
* Encryption at rest is supported for MySQL, Oracle, SQL Server, PostgreSQL, MariaDB & Aurora.
* Encryption is done using the AWS Key Management System (KMS) service.
* Once your RDS instance is encrypted, the data stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas and snapshots.

# Data Warehousing
* Used for business intelligence. Tools like Cognos, Jaspersoft, SQL Server Reporting Services, Oracle Hyperion, SAP Business Warehouse.
* Used to pull in very large and complex data sets. Usually used by management to do queries on data (such as current performance vs targets etc)

# OLTP vs OLAP
* Online Transaction Processing (OLTP) differs from Online Analytics Processing (OLAP) in terms of the types of queries you will run.

* OLTP Example:
    - Order number 2120121
    - Pulls up a row of data such as Name, Date, Address.
    - Delivery status etc.

* OLAP Transaction Example:
    - Net Profit for EMEA and Pacific for the Digital Radio Product.
    - Pulls in large numbers of records.
    - Sum of Radios Sold in EMEA
    - Sum of Radios Sold in Pacific
    - Unit Cost of Radio in each region
    - Sales price of each radio
    - Sales price - unit cost

* Data Warehousing databases use different type of architecture both from a database perspective and infrastructure layer.
* Amazon's Data Warehouse Solution is called Redshift (OLAP).
* Redshift is used for Business Intelligence or Data Warehousing.

# DynamoDB
* Stored on SSD storage.
* Spread across 3 geographically distinct data centers.
* Eventual Consistent Reads (Default)
* Strongly Consistent Reads.
* There will always be a charge for provisioning read and write capacity and the storage of data within DynamoDB

# Redshift
* Used for business intelligence.
* Available in only 1 Availability Zone.
* Backups are enabled by default with a 1 day retention period.
* Maximum backup retention period is 35 days.
* Redshift always attempts to maintain at least 3 copies of your data (the original and replica on the compute nodes and a backup in Amazon S3).
* Redshift can also asynchronously replicate your snapshots to S3 in another region for disaster recovery.

# Aurora
* 2 copies of your data are contained in each Availability Zone, with a minimum of 3 Availability Zones. Total 6 copies of your data.
* You can share Aurora snapshots with other AWS accounts.
* 3 types of replicas available. Aurora replicas, MySQL replicas & PostgreSQL replicas. Automated failover is only available with Aurora Replicas.
* Aurora has automated backups turned on by default.
* You can also take snapshots with Aurora and share these snapshots with other AWS accounts.
* Use Aurora Serverless if you want a simple, cost-effective option for infrequent, intermittent or unpredictable workloads.

# ElastiCache
* Use ElastiCache to increase database and web application performance.
* ElastiCache is a web service that makes it easy to deploy, operate, and scale an in-memory cache in the cloud.
* The service improves the performance of web applications by allowing you to retrieve information from fast, managed, in-memory caches instead of relying entirely on slower disk-based databases.
* ElastiCache is used to speed up performance of existing databases (frequent identical queries)
* ElastiCache supports two open-source in-memory caching engines:
    - Memcached:
        * If you need to scale horizontally, use Memcached.
    - Redis:
        * Multi-AZ
        * You can do backups and restores on Redis.

# EMR
* EMR is used for big data processing.
* Consists of a master node, a core node, and (optionally) a task node.
* By default, log data is stored on the master node.
* You can configure replication to S3 on give-minute intervals for all log data from the master node; however, this can only be configured when creating the cluster for the first time.

# Test Questions
* When you create a DB instance, you can choose an Availability Zone or have AWS choose one for you. An Availability Zone is represented by an AWS Region code followed by a letter identifier (for example, us-east-1a). Reference: RDS - Regions, Availability Zones, and Local Zones
* You don't need to specify a destination port number when you create DB security group rules. The port number defined for the DB instance is used as the destination port number for all rules defined for the DB security group. Reference: DB security groups
* Reserved DB instance benefits apply for both Multi-AZ and Single-AZ configurations.
* Data transferred between Availability Zones for replication of Multi-AZ deployments is free.
* RAID 0 provides performance improvements compared with a single volume as data can be read and written to multiple disks simultaneously. 2 disks, each with a bandwidth of 4,000 IOPS will provide a combined bandwidth of 8,000 IOPS.
* Provisioned IOPS becomes important when you are running production environments requiring rapid responses, such as those which run e-commerce websites. Without high performant responses from an RDS instance page loads of the website could suffer resulting in loss of business. If your workloads are not latency sensitive or you are running a test environment the additional cost of provisioned IOPS will not be cost beneficial to your project.
* Elastic Block Storage (EBS) is recommended block level storage for EC2 instances if you were running a database on an EC2 instance. 
* You cannot SSH into or control an RDS operating system. Only DB Instances deployed within a VPC can be accessed by EC2 Instances deployed in the same VPC.