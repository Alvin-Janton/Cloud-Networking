

## Testing VPC Connectivity

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service that allows you to create your own virtual private cloud network. It is useful because of its ease of use, it's cost, and its scalability.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create my own virtual private cloud network.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how easy this project would be.

### This project took me...

This project took me 40 minutes to complete.

---

## Connecting to an EC2 Instance

Connectivity is the ability for instances to be reached by traffic. Poor connectivity can lead to poor latency, and low avalability.

My first connectivity test was whether I could connect to my public ec2 instance.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

I connected to my EC2 instance using EC2 Instance Connect, which is a AWS managed service that allows secure connection to an EC2 instance, without having to manage ssh keys.

My first attempt at getting direct access to my public server resulted in an error, because my security group only allowed traffic using the http protocal. To log in to my EC2 instance, I needed to use ssh.

I fixed this error by editing my public EC2 instance's security group, and adding an inbound traffic rule to allow the ssh protocal.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

Ping is a command that sends data packets to a source using the ICMP protocol. I used ping to test the connectivity between my private and public EC2 instances.

The ping command I ran was Ping 10.0.1.113. What this command does is that it sends ICMP traffic to the specified IP address and returns the response in the terminal.

The first ping returned nothing. This meant that the traffic could not reach the private EC2 instance.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

I troubleshot this by checking my public EC2 instance's route table, security group, and network ACL. I found that my security group did not allow ICMP traffic to be sent. After fixing that, I had to look at my private EC2 instance's network resources as well. I updated the private EC2 instance's security group and NACL to fix the problem.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

Curl is a command used to test connectivity to the internet. Curl stands for Client for URL, and it works by sending an http request to a website's server.

I used curl to test the connectivity between my public EC2 instance, and the internet. I tested this by using the curl command to send traffic to websites and viewing the response.

### Ping vs Curl

Ping and curl are different because Ping sends ICMP traffic, which is similar to saying hello and waiting for a response. Curl, sends an http request, and is met with the html contents of a website.

---

## Connectivity to the Internet

I ran the command "curl learn.nextwork.org" which returned the html contents of the website. This demonstrates that my public EC2 is capable of connecting to the internet.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-connectivity_8ee57662)

---

---
