

## Build a Virtual Private Cloud (VPC)

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

