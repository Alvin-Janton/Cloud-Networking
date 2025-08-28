<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Creating a Private Subnet

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-private)

**Author:** Alvin Janton  
**Email:** alvinjanton575@gmail.com

---

## Creating a Private Subnet

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-private_afe1fdbd)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service that allows you to create a virtual private cloud network. It's useful because of its ease of use and scalability.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a VPC and add resources for my VPC network.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project is how easy it would be.

### This project took me...

This project took me 30 minutes to complete.

---

## Private vs Public Subnets

The difference between public and private subnets is that public subnets have route tables with routing rules that lead to an internet gateway. Private subnets don't have internet gateways attached to them, so they are not accessible from external entities.

Having private subnets are useful because developers may have resources that they don't want accessible to the internet, like a database to a website, or an S3 bucket.

My private and public subnets cannot have the same CIDR block. This is because, networks can get confused on where traffic is supposed to go if two subnets share the same CIDR block.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, my private subnet is associated with my route table created for my public subnet.

I had to set up a new route table because the route table expose my private subnet to external traffic, which is not what I want.

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
