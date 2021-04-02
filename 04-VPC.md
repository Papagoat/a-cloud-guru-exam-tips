# VPC
* Think of a VPC as a virtual data center in the cloud.
* Consists of IGWs (or Virtual Private Gateways), Route Tables, Network Access Control Lists, Subnets and Security Groups.
* 1 Subnet = 1 Availability Zone.
* Can have multiple Subnets in same Availability Zone.
* Security Groups are Stateful. Network Access Control Lists are Stateless.
* No Transitive Peering.
* When you create a VPC, a default Route Table, Network Access Control List (NACL) and a default Security Group will also be created.
* It won't create any Subnets or will it create a default internet gateway.
* US-East-1A in your AWS account can be a completely different availability zone to US-East-1A in another AWS account. The AZs are randomized.
* Amazon always reserve 5 IP addresses within your subnets.
* You can only have 1 Internet Gateway per VPC.
* Security Groups can't span VPCs.
* https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html

## What can we do with a VPC?
* Launch instances into a subnet of your choosing.
* Assign custom IP address ranges in each subnet.
* Configure route tables between subnets.
* Create internet gateway and attach it to our VPC.
* Much better security control over your AWS resources.
* Instance security groups.
* Subnet network access control lists (ACLS)

## Default VPC vs Custom VPC
* Default VPC is user friendly, allowing you to immediately deploy instances.
* All Subnets in default VPC have a route out to the internet.
* Each EC2 instance has both a public and private IP address.

## VPC Peering
* Allows you to connect one VPC with another via a direct network route using private IP addresses.
* Instances behave as if they were on the same private network.
* You can peer VPCs with other AWS accounts as well as with other VPCs in the same account.
* Peering is in a star configuration: ie 1 central VPC peers with 4 others. **No Transitive Peering** (You can't peer one VPC through another VPC).
* You can peer between regions.

## Nat Instances
* When creating a NAT instance, disable source/destination check on the instance.
* NAT instances must be in a public subnet.
* There must be a route out of the private subnet to the NAT instance in order for this to work.
* The amount of traffic that NAT instances can support depends on the instance size. If you are bottlenecking, increase the instance size.
* You can create high availability using Autoscaling Groups, multiple subnets in different AZs and a script to automate failover.
* Behind a Security Group.

## Nat Gateways
* Redundant inside the Availability Zone.
* can survive failure of EC2 instances.
* Cannot span Availability Zones.
* Preferred by the enterprise.
* Starts at 5Gpbs and scales currently to 45Gps.
* No need to patch.
* Not associated with Security Groups.
* Automatically assigned a public ip address.
* Remember to update your route tables.
* No need to disable Source/Destination Checks.
* If you have resource in multiple Availability Zones and they share one NAT gateway, in the event that the NAT gateway's Availability Zone is down, resources in the other Availability Zones lose internet access. To create an Availability Zone independent architecture, create a NAT gateway in each Availability Zone and configure your routing to ensure that resources use the NAT gateway in the same Availability Zone.

## Network ACLs
* Your VPC automatically comes with a default network ACL and by default, it allows all outbound and inbound traffic.
* You can create custom network ACLs. By default, each custom network ACL denies all inbound and outbound traffic until you add rules.
* Each subnet in your VPC must be associated with a network ACL. If you don't explicitly associate a subnet with a network ACL, the subnet is automatically associated with the default network ACL.
* Block IP Addresses using network ACLs not Security Groups.
* You can associate a network ACL with multiple subnets; however, a subnet can be associated with only one network ACL at a time. When you associate a network ACL with a subnet, the previous association is removed.
* Network ACLs contain a numbered list of rules that is evaluated in order, starting with the lowest numbered rule.
* Network ACLs have separate inbound and outbound rules, and each rule can either allow or deny traffic.
* Network ACLs are stateless; responses to allowed inbound traffic are subject to the rules for outbound traffic (and vice versa).

# Bastion Host
* A NET Gateway or NAT Instance is used to provide internet traffic to EC2 instances in a private subnet.
* A Bastion is used to securely administer EC2 instances (Using SSH or RDP). Bastions are called Jump Boxes in various countries.
* You cannot use a NAT Gateway as a Bastion host.

# Direct Connect
* Direct Connect directly connects your data center to AWS.
* Useful for high throughput workloads (ie lots of network traffic).
* Or if you need a stable and reliable secure connection.
* Steps:
    - Create a virtual interface in the Direct Connect console. This is a **PUBLIC Virtual Interface**.
    - Go to the VPC console and then to VPN connections. Create a Customer Gateway.
    - Create a Virtual Private Gateway.
    - Attach the Virtual Private Gateway to the desired VPC.
    - Select VPN Connections and create a new VPN Connection.
    - Select the Virtual Private Gateway and the Customer Gateway.
    - Once the VPN is available, set up the VPN on the customer gateway or firewall.

# Global Accelerator
* AWS Global Accelerator is a service in which you create accelerators to improve availability and performance of your applications for local and global users.
* You are assigned two static IP addresses (or alternatively you can bring your own).
* You can control traffic using traffic dials. This is done within the endpoint group.

# VPC Endpoints
* A VPC Endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an internet gateway, NAT device, VPN connection or AWS Direct Connect connection. Instances in your VPC do not require public IP addresses to communicate with resources in the service. Traffic between your VPC and the other service does not leave the Amazon network.
* Endpoints are virtual devices. They are horizontally scaled, redundant and highly available VPC components that allow communication between instances in your VPC and services without imposing availability risks or bandwidth constraints on your network traffic.
* There are two types of VPC endpoints:
    - Interface Endpoints
    - Gateway Endpoints (Supports Amazon S3 and DynamoDB)