# 3 Different Types of Load Balancers
* Application Load Balancers
* Network Load Balancers
* Classic Load Balancers

# Troubleshooting
* 504 Error means the gateway has timed out. This means that the application is not responding within the idle timeout period.
* Troubleshoot the application. Is it the Web Server or Database Server?
* If you need the IPv4 address of your end user, look for the X-Forwarded-For header.


# Load Balancers
* Instances monitored by ELB are reported as InService or OutofService
* Health Checks check the instance health by talking to it.
* Load Balancers have their own DNS name. You are never given an IP address.
* Read the ELB FAQ for all Load Balancers.

# Advanced Load Balancer Theory
* Sticky Sessions enable your users to stick to the same EC2 instance. Can be useful if you are storing information locally to that instance.
* Cross Zone Load Balancing enables you to load balance across multiple availability zones.
* Path patterns allow you to direct traffic to different EC2 instances based on the URL contained in the request.

# CloudFormation
* Is a way of completely scripting your cloud environment.
* Quick Start is a bunch of CloudFormation templates already built by AWS Solutions Architects allowing you to create complex environments very quickly.

# Elastic Beanstalk
* Quick deploy and manage applications in the AWS Cloud without worrying about the infrastructure that runs those applications.
* Simply upload your application and Elastic Beanstalk automatically handles the details of capacity provisioning, load balancing, scaling and application health monitoring.

# Autoscaling
## What are my scaling options?
* Maintain current instance levels at all times.
* Scale manually.
* Scale based on a schedule.
* Scale based on demand.
* Use predictive scaling.

# HA Architecture
* Always design for failure.
* Use Multiple AZs and Multiple Regions wherever you can.
* Know the difference between Multi-AZ (disaster recovery) and Read Replicas (performance) for RDS.
* Know the difference between scaling out (add additional instances) and scaling up (increase resources, e.g. t2.micro -> t3.xlarge).
* Read the questions carefully and always consider the cost element.
* Know the different S3 storage classes.

# HA with Bastion Hosts
* Two hosts in two separate AZs. - Use a Network Load Balancer with static IP addresses and health checks to fail over from one host to the other.
* Can't use an Application Load Balancer as it is layer 7 and you need to use layer 4.
* One host in one AZ behind an Auto Scaling group with health checks and a fixed EIP. If the host fails, the health check will fail and the Auto Scaling group will provision a new EC2 instance in a separate AZ. You can use a user data script to provision the same EIP to the new host. This is the cheapest option but it is not 100% fault tolerant.

# High-level AWS services you can use on-premises.
* Database Migration Service (DMS)
* Server Migration Service (SMS)
* AWS Application Discovery Service
* VM Import/Export
* Download Amazon Linux 2 as an ISO