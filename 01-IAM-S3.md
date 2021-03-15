# IAM 
* IAM consists of the following: Users, Groups, Roles, Policies.
* IAM is universal. Does not apply to regions.
* The "root account" is simply the account created when first setup your AWS account. It has complete Admin access.
* New users have **NO permissions** when first created.
* New users are assigned **Access Key ID** & **Secret Access Keys** when first created. These are not the same as a password.
* You only get to view your **Access Key ID** & **Secret Access Keys** once.
* Always setup **Multifactor Authentication** on your root account.
* You can create and customise your own password rotation policies

# S3
* S3 is Object-based. i.e. allows you to upload files.
* Files are be from 0 Bytes to 5 TB.
* There is unlimited storage.
* FIles are stored in Buckets.
* S3 is a universal namespace. Names must be unique globally.
* Not suitable to install an operating system on (Object based storage not block based).
* Successful uploads will generate a HTTP 200 status code.
* You can turn on MFA Delete.
* The Key Fundamentals of S3 are:
    - Key (Name of Object)
    - Value (The data and it is made up of a sequence of bytes)
    - Version ID (Important for versioning)
    - Metadata (Data about the data you are storing)
    - Subresources 
        - Access Control Lists (ACL. Permissions for the object) 
        - Torrent
* Read after Write consistency for PUTS of new Objects.
* Eventual Consistency for overwrite PUTS and DELETES (Can take some time to propagate).

## S3 Encryption
* Encryption in Transit is achieved by:
    - SSL/TLS
* Encryption at Rest (Server Side) is achieved by:
    - S3 Managed Keys - SSE-S3
    - AWS Key Management Service, Managed Keys - SSE-KMS
    - Server Side Encryption with Customer Provided Keys - SSE-C
* Client Side Encryption

## Sharing Buckets
* Using Bucket Policies & IAM (applies across the entire bucket). Programmatic Access only.
* Using Bucket ACLs * IAM (individual objects). Programmatic Access only.
* Cross-account IAM Roles. Programmatic AND Console access.

## Cross Region Replication
* Versioning must be enable on both the source and destination buckets.
* Files in an existing bucket are not replicated automatically.
* All subsequent updated files will be replicated automatically.
* Delete markers are not replicated.
* Deleting individual versions or delete markers will not be replicated.

## Lifecycle Policies
* Automates moving your objects between the different storage tiers.
* Can be used in conjunction with versioning.
* Can be applied to current and previous versions.

## S3 Storage Classes
* S3 Best Value
    - S3 Standard
    - S3 - IA
    - S3 - Intelligent Tiering
    - S3 One Zone - IA
    - S3 Glacier
    - S3 Glacier Deep Archive


| Type | Availability | Durability | Desc | Retrieval Fee | First byte latency |
|---|---|---|---|---|---|
| S3 Standard | 99.99% availability | 99.999999999% durability | Stored redundantly across multiple devices in multiple facilities and is designed to sustain the loss of 2 facilities concurrently | NA | milliseconds |
| S3 - IA (Infrequently Accessed) | 99.99% availability | 99.999999999% durability | For data that is accessed less frequently but requires rapid access when needed. Lower fee than S3, but you are charged a retrieval fee | per GB retrieved | milliseconds |
| S3 One Zone - IA | 99.5% availability | 99.999999999% durability | For where you want a lower-cost option for infrequently accessed data but do not require the multiple AZ data resilience | per GB retrieved | milliseconds |
| S3 Intelligent Tiering | 99.99% availability | 99.999999999% durability | Designed to optimise costs by automatically moving data to the most cost-effective access tier, without performance impact or operational overhead | NA | milliseconds |
| S3 Glacier | 99.99% availability | 99.999999999% durability | A secure, durable and low-cost storage class for data archiving. Retrieval times configurable from minutes to hours | per GB retrieved | select minutes or hours |
| S3 Glacier Deep Archive | 99.99% availability | 99.999999999% durability | Lowest-cost storage class where a retrieval time of 12 hours is acceptable | per GB retrieved | select hours |

# AWS Organisations
## Best Practices
* Always enable MFA on root account.
* Always use a strong and complex password on root account.
Paying account should be used for billing purposes only. Do not deploy resources into the paying account.
* Enable/Disable AWS services using Service Control Policies (SCP) either on OU or on individual accounts.

# Cloudfront
* Edge Location - This is the location where content will be cached. This is separate to an AWS Region/AZ.
* Origin - This is the origin of all the files that the CDN will distribute. This can be either an S3 Bucket, an EC2 Instance, an Elastic Load Balancer or Route 53.
* Distribution - This is the name given by the CDN which consists of a collection of Edge Locations.
* Web Distribution - Typically used for website.
* RTMP - Used for Media Streaming.
* Edge locations are not just READ only
* Objects are cached for the life of the TTL (Time To Live).
* You can clear cached objects but you will be charged.

# Snowball
* Import to S3
* Export to S3

# Storage Gateway
* File Gateway (NFS)
    - For flat files, stored directly on S3.
* Volume Gateway (ISCSI)
    - Stored Volumes - Entire Dataset is stored on site and is asynchronously backed up to S3.
    - Cached Volumes - Entire Dataset is stored on S3 and the most frequently accessed data is cached on site.
* Gateway Virtual Tape Library
    - Used for backup and uses popular backup applications like NetBackup, Backup Exec, Veeam etc.

# Athena
* Athena is an interactive query service.
* Allows you to query data located in S3 using standard SQL.
* Serverless.
* Commonly used to analyse log data stored in S3.

# Macie
* Macie uses AI to analyze data in S3 and helps to identify PII.
* Can also be used to analyse Cloud Trail logs for suspicious API activity.
* Includes Dashboards, Reports and Alerting.
* Great for PCI-DSS compliance and preventing ID theft.