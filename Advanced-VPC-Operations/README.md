

## VPC Monitoring with Flow Logs


---



---

## In the first part of my project...

### Step 1 - Set up VPCs

In this step, I will use the VPC Wizard to create two new VPCs in minutes.

### Step 2 - Launch EC2 instances

In this step, I will launch two EC2 instances in both VPCs public subnets.

### Step 3 - Set up Logs

In this step, I will set up VPC flow logs, and set up log analysis using CloudWatch.

### Step 4 - Set IAM permissions for Logs

In this step, I will create an IAM role to allow VPC Flow Logs to write logs and send them to CloudWatch.

---

## Multi-VPC Architecture

I started my project by launching two VPCs using the VPC Wizard.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16, and 10.2.0.0/16 respectively. They have to be unique because if two VPCs have the same CIDR block it could cause IP address collision.

### I also launched EC2 instances in each subnet

My EC2 instances' security groups allow ICMP traffic from the other VPCs CIDR block. This is because ICMP traffic is blocked by default, but I need to use the ping command to test connectivity.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-monitoring_e7fa8775)

---

## Logs

Logs are information retrieved and stored relating to actions taken in your AWS environment.

Log groups are a folder that holds logs in relation to a specific resource or resources.

### I also set up a flow log for VPC 1

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-monitoring_e8398869)

---

## IAM Policy and Roles

I created an IAM policy because VPC Flow Logs do not have permission to write logs to CloudWatch.

I also created an IAM role because VPC Flow Logs requires an IAM role to function.

A custom trust policy is an IAM policy that is used to define a specfic resource in the AWS environment. Flow Logs aren't an independent resource, so to create a role for it we have to create a custom trust policy with vpc-flow-logs as the principal.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-monitoring_4334d777)

---

## In the second part of my project...

### Step 5 - Ping testing and troubleshooting

In this step, I will attempt to generate logs by sending traffic from VPC-1 to VPC-2.

### Step 6 - Set up a peering connection

In this step, I will create a VPC peer connection between the two VPCs, then I'll update the route table to add a route.

### Step 7 - Analyze flow logs

In this step, I will review the flow logs recorded about VPC-1's public subnet. Furthermore, I will analyse the logs to get more insight on the traffic.

---

## Connectivity troubleshooting

My first ping test between my EC2 instances had no replies, which means that there is no connection between the two EC2 instances.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-monitoring_99d4ba42)

I could receive ping replies if I ran the ping test using the other instance's public IP address, which means the security group is correctly configured to allow ICMP traffic.

---

## Connectivity troubleshooting

Looking at VPC 1's route table, I identified that the ping test with Instance 2's private address failed because I didn't have a peering connection route in my route table, so the EC2 instance didn't know where to send the traffic.

### To solve this, I set up a peering connection between my VPCs

I also updated both VPCs' route tables to add a new rule allowing the VPCs to send traffic between one another.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-monitoring_7316a13d)

---

## Connectivity troubleshooting

I received ping replies from Instance 2's private IP address! This means that the two VPCs can successfully communicate with each other.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-monitoring_4ec7821f)

---

## Analyzing flow logs

Flow logs tell give use information surrounding the details of traffic going into and out of a public subnet.

For example, the flow log I've captured tells us about the ssh connection attempts, and the ICMP traffic I sent.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-monitoring_d116818e)

---

## Logs Insights

Logs Insights can take log data from a log group and allow you to run queries to find specific information in logs.

I ran the query " stats sum(bytes) as bytesTransferred by srcAddr, dstAddr
| sort bytesTransferred desc
| limit 10" .
This query analyzes the top 10 largest traffic transfered in bytes, as well as finding the source, and desitination IP addresses involved in the transaction.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-monitoring_3e1e79a1)

---

---
