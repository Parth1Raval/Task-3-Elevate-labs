# Task-3-Elevate-labs

**Step-by-Step Guide: AWS VPC with Public and Private Subnets**

This guide will help you learn how cloud networking works by walking you through creating a Virtual Private Cloud (VPC) in AWS with both public and private subnets, plus controlled internet access. Each step explains not just "how," but also "why"—so you understand the basics of secure cloud architectures and resource isolation.

1. Login and Open VPC Dashboard
Sign in to your AWS Management Console.

In the search bar, type VPC, then click the VPC Dashboard.
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

2. Create a New VPC
Click Create VPC.

Name it (e.g., my-first-vpc).

Set IPv4 CIDR block to 10.0.0.0/16 (this defines your cloud's private address space; enough for multiple subnets).

Leave other options as default and click Create.

Checkpoint: Can you explain what a CIDR block is and why it's important? (Tip: It sets the range of private IPs your cloud uses.)
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

3. Create Two Subnets
Go to Subnets > Create subnet.

Public Subnet

Name: public-subnet

IPv4 CIDR block: 10.0.1.0/24

Select an Availability Zone

Click Create, then Edit subnet settings > Auto-assign public IP: set to Enable

Private Subnet

Name: private-subnet

IPv4 CIDR block: 10.0.2.0/24

Select an Availability Zone

Click Create, then Edit subnet settings > Auto-assign public IP: set to Disable

Check-In: Why would you want to disable public IPs in a private subnet?
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

4. Set Up an Internet Gateway (IGW)
Go to Internet Gateways > Create internet gateway (name it, e.g., my-vpc-igw).

Click Attach to VPC and choose your VPC.

Hint: IGWs allow resources in your VPC to connect to the internet.
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

5. Configure Route Tables
Go to Route Tables > Create route table.

Public Route Table:

Name: public-route-table

Associate with your VPC

In the Routes tab: Add 0.0.0.0/0 as destination ⇒ Target: your IGW

In Subnet Associations: Associate this table with your public subnet only

Private Route Table:

Name: private-route-table

Associate with your VPC

Leave only the local route (typically 10.0.0.0/16)—no route for 0.0.0.0/0

In Subnet Associations: Associate only the private subnet
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

6. Verify Configuration
Go to Subnets and check:

Public subnet: Has public route table, auto-assign public IP is enabled, should allow internet access

Private subnet: Has private route table, no internet route—should be isolated
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Why is This Important?
This pattern (public + private subnets) is the backbone of secure cloud architecture.

Public subnets host servers that need internet, like web servers.

Private subnets protect sensitive resources, like databases, by keeping them off the public internet.

Route tables and the IGW carefully control access between subnets and the outside world.

Tip: Try launching a test EC2 instance in each subnet. Only the one in the public subnet should get a direct public IP and reach the internet.
