

## VPC Traffic Flow and Security

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service that lets you create a virtual private cloud network. It is useful because of its ease of use.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a VPC, subnet, internet gateway, route table, security group, and network ACL.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how easy this project was going to be.

### This project took me...

This project took me one hour to complete.

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

---
