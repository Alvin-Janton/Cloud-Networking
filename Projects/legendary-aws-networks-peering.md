

## VPC Peering


---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service that allows you to create a virtual private cloud network. It is useful because of its ease of use, cost, and scalability.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create my own virtual private cloud network.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how easy this project ended up being.

### This project took me...

This project took me 45 minutes to complete.

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, I will use the VPC Wizard to create two new VPCs in minutes.

### Step 2 - Create a Peering Connection

In this step, I will set up a connection link between the two newly created VPCs.

### Step 3 - Update Route Tables

In this step, I will configure the route table to allow traffic to flow between the two VPCs.

### Step 4 - Launch EC2 Instances

In this step, I will launch an EC2 instance in both of my VPCs public subnets.

---

## Multi-VPC Architecture

I started my project by launching two VPCs using the VPC Wizard tool.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16, and 10.2.0.0/16 respectively. They have to be unique because if VPCs have overlapping CIDR blocks, then they might use the same IP addresses which will cause confusion.

### I also launched 2 EC2 instances

I didn't set up key pairs for these EC2 instances as AWS has a service called EC2 Connect, which allows for secure login into EC2 instances using AWS managed SSH keys.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is a connection between two independent VPCs, that allows them to communicate with each other.

A peering connection lets VPCs and their resources route traffic between them using their private IP addresses. This means data can now be transferred between VPCs without going through the public internet.

The difference between a Requester and an Accepter in a peering connection is the Requester is the VPC that is sending the connection request to another VPC. The accepter is the VPC which is accepting the request.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting a peering connection, my VPCs' route tables need to be updated because even with a connection, VPCs don't know how to route traffic to the other VPC.

Format your response as 'My VPCs' new routes have a destination of the other VPCs CIDR block. The routes' target was the peering connection between the two.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I will use EC2 Connect to connect to my VPC-1 EC2 instance.

### Step 6 - Connect to EC2 Instance 1

In this step, I will try to connect to my EC2 instance again, and fix another error.

### Step 7 - Test VPC Peering

In this step, I will attempt to send traffic from instance 1 to instance 2, and fix any errors that occur.

---

## Troubleshooting Instance Connect

Next, I used EC2 Instance Connect to my EC2 instance for VPC-1.

I was stopped from using EC2 Instance Connect as I didn't have a public IP address allocated to my EC2 instance. For EC2 Connect to work, it needs to connect to the instance's public ip over the internet.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolve this error, I set up Elastic IP addresses. Elastic IP addresses are static IP addresses that can be attached to an EC2 instance after it has already launched. Allowing for EC2 Connect to work.

Associating an Elastic IP address resolved the error because now, EC2 Connect has a public IP address that it can connect to.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, I used the Ping command to send traffic to the private ipv4 address of of the VPC-2 EC2 instance. The Ping command sends ICMP traffic to a specified IP address, this allows me to check whether the two instances can communicate.

A successful ping test would validate my VPC peering connection because it shows that the two EC2 instances can communicate back and forth.

I had to update my second EC2 instance's security group because it blocked ICMP traffic by defualt. I added a new rule that allowed ICMP traffic from the CIDR block from VPC-1.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-peering_7a29d352)

---

---
