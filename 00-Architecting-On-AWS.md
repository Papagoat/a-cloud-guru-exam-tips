# Amazon S3
* 11 9s durability
* Globally Unique and DNS Compliant
* Virtual Hosted Style - https://[bucket name].s3.amazonaws.com
* Key Name - File Name
* Different storage classes - https://aws.amazon.com/s3/storage-classes/?nc=sn&loc=3
* Different pricing - https://aws.amazon.com/s3/pricing/

## Mechanical Sympathy
https://wa.aws.amazon.com/wat.concept.mechanical-sympathy.en.html

## Well Architected
https://aws.amazon.com/architecture/well-architected

## Policy Generator
https://awspolicygen.s3.amazonaws.com/policygen.html

## Amazon Glacier
* Standard retrieval - 3 to 5 hours
* Expedited retrieval - 1 - 5 hours
* Bulk retrieval - 12 hours

## S3 Storage Classes
* 4 9s availability (99.99%) Potential downtime - Less than 53 mins per year

# EC2
## Meta Data
* Get user data - http://169.254.169.254/latest/user-data
* Get meta data - http://169.254.169.254/latest/meta-data
* Get host name - http://169.254.169.254/latest/hostname
* Get mac address - http://169.254.169.254/latest/mac

## Elastic Block Store
* Block level storage
* Is not an instance store (Ephemeral)
* Attaches to a network
* Not shared storage
* Different volume types - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html
* Replicated for redundancy

## Why are they called Elastic?
* You can change configuration and provision.
* EFS - Grows as you put files on it.

## Storage patterns
https://aws.amazon.com/blogs/storage/comparing-your-on-premises-storage-patterns-with-aws-storage-services/

## Instance types
https://aws.amazon.com/ec2/instance-types/

## Spot instance interruptions
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/spot-interruptions.html

## Differences between Dedicated Hosts and Dedicated Instances
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-hosts-overview.html#dedicated-hosts-dedicated-instances

# Database
## Relational
* RDS OLTP - Transaction
* Redshift OLAP - Analytics
* Aurora

## Non Relational
* Dynamo DB
* ElasticCache
* Neptune
* DocumentDB

* DynamoDB - Read & Write configuration

# Network
* 10.0.0.0: Network address.
* 10.0.0.1: Reserved by AWS for the VPC router.
* 10.0.0.2: Reserved by AWS. The IP address of the DNS server is the base of the VPC network range plus two. For VPCs with multiple CIDR blocks, the IP address of the DNS server is located in the primary CIDR. We also reserve the base of each subnet range plus two for all CIDR blocks in the VPC. For more information, see Amazon DNS server.
* 10.0.0.3: Reserved by AWS for future use.
* 10.0.0.255: Network broadcast address. We do not support broadcast in a VPC, therefore we reserve this address.

## Create Public Subnet
* Create an internet gateway<
* Create a route table<
* Add a route to the route table that directs 0.0.0.0/0< traffic to the internet gateway<
* Associate the route table with a subnet, which therefore becomes a public subnet

## Elastic IP Address
Static public IP Address but can move across regions

## Ephermeral Ports
https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html#nacl-ephemeral-ports

## Control Tower
https://aws.amazon.com/controltower/faqs/

## Direct Connect Partners
https://aws.amazon.com/directconnect/partners/?nc=sn&loc=7&dn=1

## Create VPC endpoints without internet access
https://aws.amazon.com/premiumsupport/knowledge-center/ec2-systems-manager-vpc-endpoints/

# Load Balancer
https://aws.amazon.com/elasticloadbalancing/features/?nc=sn&loc=2&dn=1
https://aws.amazon.com/blogs/aws/introducing-aws-gateway-load-balancer-easy-deployment-scalability-and-high-availability-for-partner-appliances/

# Protocols
ALB - L7 - HTTP, HTTPS, gRPC	
NLB - L4 - TCP, UDP, TLS


# IAM
https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_identity-vs-resource.html
https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html
https://docs.aws.amazon.com/general/latest/gr/root-vs-iam.html#aws_tasks-that-require-root

# Automation
https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/sample-templates-services-us-west-2.html#w2ab1c36c58c13c17
https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html

# Caching
https://aws.amazon.com/elasticache/redis-vs-memcached/
https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/Replication.Redis-RedisCluster.html

# Certification
https://aws.amazon.com/certification/certified-solutions-architect-associate/
Exam Readiness

```
#!/bin/bash
yum update -y
yum install -y httpd.x86_64
systemctl start httpd.service
systemctl enable httpd.service
echo "Hello World from $(hostname -f)" > /var/www/html/index.html
```