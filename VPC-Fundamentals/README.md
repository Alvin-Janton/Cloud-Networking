

## Build a Virtual Private Cloud (VPC)

---

![Architecture](https://github.com/Alvin-Janton/Cloud-Networking/blob/face50d9d252bca4b826c5d5d107c4f51d0719ff/images/architecture.png?eaw=true)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a resource that lets you create a virtual private cloud network. It is useful because it simplifies the process of creating all the necessary resources to create a network, like subnets, internet gateways, and VPCs.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create my own VPC, subnet, and internet gateway. 

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how simple the process would be.

### This project took me...

This project took me one two hours to complete.

---

## Virtual Private Clouds (VPCs)

VPCs are private personal networks that are used to contian, and manage access to resources. The owner has full discretion over these resources, and can choose how to configure them, their access specifications, and their security rules.

When I checked the Your VPCs section, I noticed there was already a default VPC in my account. This is because AWS sets up a VPC for an account when it is first created. If you don't have a VPC you won't be able to use any of the resources that require one to operate like EC2, or databases.

To set up my VPC, I had to define an IPv4 CIDR block. CIDR stands for Classless Inter-Domain Routing, and they're used to define the number of IP addresses within a network. To understand how big a CIDR block is, look at the number after the slash - the smaller the number, the larger the CIDR block! For example, 10.0.0.0/16 means the first 16 bits of your IP address (10.0) are fixed, but the remaining 16 bits can be allocated however you like. Addresses within this CIDR block start at 10.0.0.0 and go up to 10.0.255.255. 

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-vpc_2facf927)

---

## Subnets

Subnets are sections within a VPC that have their own resources and rules configured by the owner. There are already subnets existing in my account, one for every avaliablilty zone (AZ) in my region. An AZ is the location where a data center lies within a specific region. For example, my region is us-east-1, there are 6 AZs total in this region.

Once I created my subnet, I enabled the option to have a public IPV4 added to the subnet. This setting makes sure that my subnet's EC2 instances will be accessible from the internet.

The difference between public and private subnets is the ability to be accessed from the internet. For a subnet to be considered public, it has to have an internet gateway attached to it. Public subnets are used when you want to create a resource that can be accessed from the internet like an EC2 instance. Private subnets are used when you create a resource that you don't want accessed from the internet, like a database. 

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-vpc_157c4219)

---

## Internet gateways

An internet gateway connects VPCs to the internet. Internet gateways are key to making applications available on the internet. By attaching an internet gateway, your instances can access the internet and be accessible to external users. If I missed this step then, none of the resources in my VPC would be able to communicate with any external entities.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-vpc_4ae90410)

---

## Using the AWS CLI

VPC resources could also be created with CloudShell, which is grants access to the CLI.  AWS CLI is a terminal that can be used to create resources in your AWS environment using commands. CLI is usually much faster than using a GUI, and it allows for task automation through running script files.

To set up a VPC or a subnet, you can use the command "aws ec2 create-subnet --vpc-id VPC-ID --cidr-block ADD-CIDR-BLOCK-HERE". Make sure to avoid errors by including the correct parameters, and make sure that your  subnet's CIDR block is within your VPC CIDR block's range.

Compared to using the AWS Console, an advantage of using commands is speed and automation. An advantage of using the Console is ease of use. Overall, I preferred using the console as it's easier to configure resources.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-vpc_9b2465411)

---



## VPC Traffic Flow and Security

---

![Archetecture](https://github.com/Alvin-Janton/Cloud-Networking/blob/93fa7d7cd592c5aaecd416c33e441771b7f8e785/images/architecture2.png?raw=true)

---

## Route tables

Route tables are tables with rules that define where traffic should go within a subnet. Route table rules are called routes.

Routes tables are needed to make a subnet public because when a route table has a route that directs traffic to an internet gateway, a subnet becomes public. Without the route table, the subnet wouldn't know where to direct the traffic.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-security_0a07b191)

---

## Route destination and target

Routes are defined by their destination and target, which mean the IP address where the traffic is coming from (destination) and the resource that the traffic wants to reach (target). In my case, the target is the internet gateway.

The route in my route table that directed internet-bound traffic to my internet gateway had a destination of 0.0.0.0/16 and a target of igw-044dabd3d423a57e1 which is my internet gateway ID. The IP address means that it is avaliable to all IPv4 IP addresses.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-security_0a07b191)

---

## Security groups

Security groups are rules that defines the type of traffic that is allowed to access your resources. Every resource must be associated with a security group. This means security groups don't attach to a VPC or a subnet, they attach to a specific resource within that VPC/subnet. If you don't specify a security group when you launch a resource, it will use the default security group that AWS creates whenever you set up a VPC.

### Inbound vs Outbound rules

Inbound rules define who can access your resources, I  configured an inbound rule that allows HTTP traffic from anywhere in the world. HTTP is a protocol that is used to send data over network on the internet.

Outbound rules define what traffic can leave your network. By default, my security group's outbound rule is that any traffic is allowed to leave my network on any port, using any protocol.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-security_92b0b0b4)

---

## Network ACLs

Network ACLs are list that have rules that define what traffic is allowed to do within a subnet. 

### Security groups vs. network ACLs

The difference between a security group and a network ACL is that unlike security groups, network ACLs work on the subnet level instead of on individual resources. This means their rules apply throughout the entire subnet, regardless of where the traffic is flowing.

---

## Default vs Custom Network ACLs

### Similar to security groups, network ACLs use inbound and outbound rules

By default, a network ACL's inbound and outbound rules will deny all inbound and outbound traffic.

In contrast, a custom ACL’s inbound and outbound rules are automatically set to allow all inbound and outbound traffic.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-security_4faeb056)

---

## Tracking VPC Resources

I created a new VPC, with an internet gateway, and a security grouup. Instead of my usual region, I used us-east-2. Teams would use multiple regions to deliver high avaliability, and fast access to their products.

EC2 Global View is a tool where you can find all of your deployed resources across all of AWS's regions. I could even narrow down my search by specific resources. Without EC2 Global View, you'd have to check each region manually to find, or check resources.

Now that I've learnt about EC2 Global View, I'd use it again if I ever do a mulit-region deployment of resources.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-security_b03ea6162)

---



## Creating a Private Subnet


---



---

## Private vs Public Subnets

The difference between public and private subnets is that public subnets have route tables with routing rules that lead to an internet gateway. Private subnets don't have internet gateways attached to them, so they are not accessible from external entities.

Having private subnets are useful because developers may have resources that they don't want accessible to the internet, like a database to a website, or an S3 bucket.

My private and public subnets cannot have the same CIDR block. This is because, networks can get confused on where traffic is supposed to go if two subnets share the same CIDR block.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, my private subnet is associated with my route table created for my public subnet.

I had to set up a new route table because the public route table exposes my private subnet to external traffic.

My private subnet's dedicated route table only has one inbound and one outbound rule that allows for internal movement within my AWS environment.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

By default, my private subnet is associated with my public NACL.

I set up a dedicated network ACL for my private subnet because it adds an extra layer of security. If one of my public facing resources was compromised, threat actors could try to compromise more of my network.

My new network ACL has two simple rules - deny all inbound traffic, and deny all outbound traffic.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-private_1ed2cb07)

---

---



