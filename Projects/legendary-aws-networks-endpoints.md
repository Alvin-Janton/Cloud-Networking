

## VPC Endpoints


---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service that allows you to create a virtual private cloud network. It is useful because of its ease of use, its cost, and its scalability.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create my own virutal private cloud network.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how easy it would be.

### This project took me...

This project took me 1 hour to complete.

---

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I will create a VPC, launch an EC2 instance, and create an S3 bucket.

### Step 2 - Connect to EC2 instance

In this step, I will connect to my EC2 instance using AWS configure.

### Step 3 - Set up access keys

In this step, I will create access keys, and use them to configure access to my account.

### Step 4 - Interact with S3 bucket

In this step, I will connect to my S3 bucket.

---

## Architecture set up

I started my project by launching a VPC, a subnet, a security group, and an EC2 instance.

I also set up an S3 bucket, and placed 4 files inside to act as data objects.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-endpoints_4334d777)

---

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I configured my user credentials using aws configure.

Access keys are passwords that allow you to grant access to your AWS environment to an external host.

Secret access keys are credentials that allow external host to connect to your instance.

### Best practice

Although I'm using access keys in this project, a best practice alternative is to use one of the recommended solutions offered by AWS.

---

## Connecting to my S3 bucket

The command I ran was aws s3 ls. This command is used to list all of the S3 buckets that exist within your account.

The terminal responded with nothing. This indicated that the access keys I set up were successful.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-endpoints_4334d778)

---

## Connecting to my S3 bucket

I also tested the command aws s3 ls s3://alvin-final-report ls command, which returned all of the objects stored within that bucket.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-endpoints_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command sudo touch tmp.test.txt. This command creates an empty file in the tmp folder.

The second command I ran was "aws s3 cp /tmp/nextwork.txt s3://alvin-final-report" This command will send a copy of the text file into my S3 bucket.

The third command I ran was aws s3 ls s3:alvin-final-report which validated that the object successfully uploaded to the bucket.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-endpoints_3e1e79a2)

---

## In the second part of my project...

### Step 5 - Set up a Gateway

In this step, I will set up a VPC endpoint.

### Step 6 - Bucket policies

In this step, I'm going to configure bucket policies to block all traffic, except for traffic coming from VPC endpoint. 

### Step 7 - Update route tables

In this step, I will attempt to connect to my S3 bucket through my EC2 instance.

### Step 8 - Validate endpoint conection

In this step, I will attempt again to connect to my S3 bucket from my EC2 instance.

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

---
