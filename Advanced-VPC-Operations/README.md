

## VPC Monitoring with Flow Logs


---

![Architecture](https://github.com/Alvin-Janton/Cloud-Networking/blob/fa567f8096e259104b89bf1a0d1cc7d834647d07/images/architecture10.png?raw=true)

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



## Access S3 from a VPC


---

![Architecture](https://github.com/Alvin-Janton/Cloud-Networking/blob/c99ba57006330f7587d7688adc991577dafd6d9d/images/architecture9.png?raw=true)

---

## Architecture set up

I started my project by launching a public EC2 instance.

I also set up an S3 bucket and added four files to act as data objects.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-s3_4334d777)

---

## Running CLI commands

AWS CLI is a tool that lets you run commands that affect your AWS environment in a terminal called CloudShell. I have access to AWS CLI because all EC2 instances use AWS CLI as their terminal.

The first command I ran was aws s3 ls. This command is used to list all of the S3 buckets that currently reside in my AWS account.

The second command I ran was aws configure This command is used to configure credentials onto a host.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-s3_e7fa8776)

---

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I configured credentials for my AWS User account using the AWS configure command and pasting my access key, and secret access key.

Access keys are similar to a username and password, they allow for access to your AWS user to an external host.


### Best practice

Although I'm using access keys in this project, a best practice alternative is to use AWS CLI V2 and enable authentication through an IAM user.

---


## Connecting to my S3 bucket

The first command I ran was aws s3 ls. This command is used to list all of the S3 buckets that currently reside in my AWS account.

Format your response as 'When I ran the command aws s3 ls again, the terminal responded with a list of all the s3 buckets that I had in my account. This indicated that I successfully configured credentials.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-s3_4334d778)

---

## Connecting to my S3 bucket

Another CLI command I ran was " aws s3 ls s3://alvin-final-report" which returned all of the objects within the specified S3 bucket.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-s3_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command " sudo touch /tmp/test.txt" .
This command creates an empty txt file in the tmp folder.

The second command I ran was " aws s3 cp /tmp/test.txt s3://alvin-final-report". This command will send a copy of the text file from the tmp directory to my S3 bucket.

The third command I ran was " aws s3 ls s3://alvin-final-report" which validated that the file was successfully uploaded to S3.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-s3_3e1e79a2)

---

## VPC Endpoints


---



---


## Setting up a Gateway

A Gateway is a type of endpoint used specifically for Amazon S3 and DynamoDB (DynamoDB is an AWS database service). Gateways work by simply adding a route to your VPC route table that directs traffic bound for S3 or DynamoDB to head straight for the Gateway instead of the internet.

### What are endpoints?

An endpoint is a service that allowes VPCs to route traffic directly to the intended service instead of to the internet gateway. This way, my EC2 instance won't have to communicate over the internet.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-endpoints_09bcaa8a)

---

## Bucket policies

A bucket policy is a piece of code that defines that actions that are allowed to occur within an S3 bucket.

My bucket policy will block all traffic except, that which is coming from the endpoint specified.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-endpoints_7316a13d)

---

## Bucket policies

Right after saving my bucket policy, my S3 bucket page showed 'denied access' warnings. This was because my policy denies all traffic attempts not from the specified endpoint. This includes my AWS account.

I also had to update my route table because it currently didn't have any routes that allowed the EC2 instance to connect to the S3 bucket without going through the internet.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-endpoints_4ec7821f)

---

## Route table updates

To update my route table, I went to my endpoint and clicked on the route table tab. From there I selected the route table for my subnet and clicked " Modify route table" to add a new route.

After updating my public subnet's route table, my terminal could return the objects in my S3 bucket after running the command " aws s3 ls s3://alvin-final-report".

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-endpoints_d116818e)

---

## Endpoint policies

An endpoint policy is a block of code that defines the actions that the endpoint will allow. You can block use of endpoint or limit it to specific accounts.

I updated my endpoint's policy by changing the Effect from Allow to Deny. I could see the effect of this right away, because when I ran the command to see the objects in my bucket again, I was denied.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-endpoints_3e1e79a3)

---





