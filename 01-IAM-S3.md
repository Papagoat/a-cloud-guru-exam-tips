# IAM 
* IAM consists of the following: Users, Groups, Roles, Policies.
* IAM is universal. Does not apply to regions.
* The "root account" is simply the account created when first setup your AWS account. It has complete Admin access.
* New users have **NO permissions** when first created.
* New users are assigned **Access Key ID** & **Secret Access Keys** when first created. These are not the same as a password.
* You only get to view your **Access Key ID** & **Secret Access Keys** once.
* Always setup **Multi-factor Authentication** on your root account.
* You can create and customize your own password rotation policies

# S3
* S3 is Object-based. i.e. allows you to upload files.
* Files are be from 0 Bytes to 5 TB.
* There is unlimited storage.
* Files are stored in Buckets.
* S3 is a universal namespace. Names must be unique globally.
* Not suitable to install an operating system on (Object based storage not block based).
* Successful uploads will generate a HTTP 200 status code.
* You can turn on MFA Delete.
* The Key Fundamentals of S3 are:
    - Key (Name of Object)
    - Value (The data and it is made up of a sequence of bytes)
    - Version ID (Important for versioning)
    - Metadata (Data about the data you are storing)
    - Sub-resources 
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
| S3 One Zone - IA | 99.5% availability | 99.999999999% durability | For where you want a lower-cost option for infrequently accessed data but do not require the multiple Availability Zone data resilience | per GB retrieved | milliseconds |
| S3 Intelligent Tiering | 99.99% availability | 99.999999999% durability | Designed to optimize costs by automatically moving data to the most cost-effective access tier, without performance impact or operational overhead | NA | milliseconds |
| S3 Glacier | 99.99% availability | 99.999999999% durability | A secure, durable and low-cost storage class for data archiving. Retrieval times configurable from minutes to hours | per GB retrieved | select minutes or hours |
| S3 Glacier Deep Archive | 99.99% availability | 99.999999999% durability | Lowest-cost storage class where a retrieval time of 12 hours is acceptable | per GB retrieved | select hours |

# AWS Organizations
## Best Practices
* Always enable MFA on root account.
* Always use a strong and complex password on root account.
Paying account should be used for billing purposes only. Do not deploy resources into the paying account.
* Enable/Disable AWS services using Service Control Policies (SCP) either on OU or on individual accounts.

# CloudFront
* Edge Location - This is the location where content will be cached. This is separate to an AWS Region/Availability Zone.
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
* Commonly used to analyze log data stored in S3.

# Macie
* Macie uses AI to analyze data in S3 and helps to identify PII.
* Can also be used to analyze Cloud Trail logs for suspicious API activity.
* Includes Dashboards, Reports and Alerting.
* Great for PCI-DSS compliance and preventing ID theft.

# Quiz
1. You are a security administrator working for a hotel chain. You have a new member of staff who has started as a systems administrator, and she will need full access to the AWS console. You have created the user account and generated the access key id and the secret access key. You have moved this user into the group where the other administrators are, and you have provided the new user with their secret access key and their access key id. However, when she tries to log in to the AWS console, she cannot. Why might that be?
    - You cannot log in to the AWS console using the Access Key ID / Secret Access Key pair. Instead, you must generate a password for the user, and supply the user with this password and your organization's unique AWS console login URL.
2. Power User Access allows ____.
    - Access to all AWS services except the management of groups and users within IAM.
3. You are a solutions architect working for a large engineering company that are moving from a legacy infrastructure to AWS. You have configured the company's first AWS account and you have set up IAM. Your company is based in Andorra, but there will be a small subsidiary operating out of South Korea, so that office will need its own AWS environment. Which of the following statements is true?
    - You will need to configure Users and Policy Documents only once, as these are applied globally.
    - IAM is a Global service. You can have regional conditions in policies, however by default users & policies are Global. https://aws.amazon.com/blogs/security/easier-way-to-control-access-to-aws-regions-using-iam-policies/
4. When you create a new user, that user ____.
    - Will be able to interact with AWS using their access key ID and secret access key using the API, CLI, or the AWS SDKs assuming programmatic access was enabled.
5. Which of the following is not a feature of IAM?
    - IAM allows you to set up biometric authentication, so that no passwords are required.
    - AWS makes use of Accounts & Passwords, or Keys and Secret keys, and MFA, to prove identity. You may have a 3rd party device that uses BioMetrics to initiate and exchange of the password or secret key with AWS, but that is not an AWS / IAM service. https://aws.amazon.com/iam/features/
6. You are a developer at a fast-growing startup. Until now, you have used the root account to log in to the AWS console. However, as you have taken on more staff, you will need to stop sharing the root account to prevent accidental damage to your AWS infrastructure. What should you do so that everyone can access the AWS resources they need to do their jobs?
    - Create a customized sign-in link such as "yourcompany.signin.aws.amazon.com/console" for your new users to use to sign in with.
    - Create individual user accounts with minimum necessary rights and tell the staff to log in to the console using the credentials provided.
7. A __ is an object in AWS stored as a JSON document that provides a formal statement of one or more permissions.
    - Policy
    - A policy is an object in AWS that, when associated with an identity or resource, defines their permissions. Most policies are stored in AWS as JSON documents.
8. A new employee has just started work, and it is your job to give her administrator access to the AWS console. You have given her a user name, an access key ID, a secret access key, and you have generated a password for her. She is now able to log in to the AWS console, but she is unable to interact with any AWS services. What should you do next?
    - Grant her Administrator access by adding her to an Administrators' group.
    - By default new user accounts come with no permission to interact with services. These must be explicitly assigned by adding a Policy or adding them to a Group.
9. Which of the following is not a component of IAM?
    - Organizational Units
    - Correct. 'OUs' are a feature of AWS Organizations https://aws.amazon.com/iam/faqs/ https://aws.amazon.com/organizations/features/
10. Every user you create in the IAM systems starts with ____.
    - No Permissions
    - AWS systems are designed to be secure 1st. The system administrator needs to add permissions to allow accounts to take actions.
11. Which statement best describes IAM?
    - IAM allows you to manage users, groups, roles, and their corresponding level of access to the AWS Platform.
12. In what language are policy documents written?
    - JSON
13. An application you are working on has a new app. The development team for this app requires access to a bucket that is located within your team's aws account. The other team requires programmatic and console level access to your team's bucket. How would you share this bucket with this other team's account?
    - Setting up a cross account IAM Role
    - Setting up a cross account IAM role is currently the only method that will allow IAM users to access cross account S3 buckets both programmatically and via the AWS console.
14. You have a client who is considering a move to AWS. In establishing a new account, what is the first thing the company should do?
    - Set up an account using their company email address.
    - This email address is a key part of linking the AWS account to your company. Using a private email address may make it harder to establish ownership if your need help from AWS. https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/ https://aws.amazon.com/blogs/security/getting-started-follow-security-best-practices-as-you-configure-your-aws-resources/ Explanation
15. You have created a new AWS account for your company, and you have also configured multi-factor authentication on the root account. You are about to create your new users. What strategy should you consider in order to ensure that there is good security on this account.
    - Enact a strong password policy: user passwords must be changed every 45 days, with each password containing a combination of capital letters, lower case letters, numbers, and special symbols.
    - A password policy to set a minimum standard is good practice and is generally a top requirement for any industry compliance endorsement. https://aws.amazon.com/blogs/security/getting-started-follow-security-best-practices-as-you-configure-your-aws-resources/
16. What is the default level of access a newly created IAM User is granted?
    - No access to any AWS services.
    - By default new IAM Users have no permissions to AWS services. They must be explicitly granted.
17. What level of access does the "root" account have?
    - Administrator Access
    - The root account in an AWS account represents the Owner of the account and can do anything including changing billing details and even close the account. The details for this account should be locked away and only used when absolutely necessary. https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html
18. What is an additional way to secure the AWS accounts of both the root account and new users alike?
    - Implement Multi-Factor Authentication for all accounts.
    - MFA provides an additional requirement for the person signing on to prove that they are who they claim to be. Username & password are things you 'know' the MFA is something that you 'have'. e.g. you have the only device that can generate the token. https://aws.amazon.com/iam/features/mfa/