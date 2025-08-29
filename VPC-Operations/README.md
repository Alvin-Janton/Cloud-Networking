

## Launching VPC Resources


---

![Architecture](https://github.com/Alvin-Janton/Cloud-Networking/blob/52567aa8c5cf70c02dfbd4a684df44017f25e8e8/images/architecture5.png?raw=true)

---

## Setting Up Direct VM Access

Directly accessing a virtual machine means using ssh to log into the instance, either through the terminal or a GUI.

### SSH is a key method for directly accessing a VM

SSH traffic means secure shell, and it is a protocol used to securely connect to resources using key pairs. SSH uses encryption algorithms to protect the confidentiality of data being transmitted between a user and a resource.

### To enable direct access, I set up key pairs

Key pairs are a tool that is used to facilitate ssh connections. Key pairs have two keys, a public key that is held onto by the instance, and a private key, which is owned by the user. Only the private key can match and connect with its corresponding public key.

A private key's file format is the encryption algorithm used to create the key. My private key's file format was RSA, a common encryption algorithm used for key pairs.

---

## Launching a public server

I had to change my EC2 instance's networking settings by selecting my VPC network instead of the deafault.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-ec2_88727bef)

---

## Launching a private server

My private server has its own dedicated security group because the default security group and the one I created for my public subnet allow access to resources through external entities. This is fine for public facing applications, but for private resources I have to configure my own security rules.

My private server's security group's source is the security group connected to the public subnet. This means that external users accessing my public EC2 will be able to access resources from my private EC2. This is more secure than allowing access from anywhere in the world.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-ec2_4a9e8014)

---

## Speeding up VPC creation

I used an alternative way to set up an Amazon VPC! This time, I used the VPC Wizard to create an entire VPC in minutes.

A VPC resource map is a visual that lets you see how resources are connected within your VPC network.

My new VPC has a CIDR block of 10.0.0.0/16 It is possible for my new VPC to have the same IPv4 CIDR block as my existing VPC because, VPCs do not occupy the same network space, so they don't communicate unless connected.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-ec2_1cbb1b88)

---

## Speeding up VPC creation

### Tips for using the VPC resource map

When determining the number of public subnets in my VPC, I only had two options 0 or 2. This was because the VPC Wizard is meant to be quick and simple, limiting the number of subnets makes that easy. The two subnets are a public and private pair. 

The set up page also offered to create NAT gateways, which are services that allow private subnets to access the internet without being exposed to external users.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-ec2_8ee57662)

---



## Testing VPC Connectivity

---



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


