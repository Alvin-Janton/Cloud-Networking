<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Access S3 from a VPC

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-s3)

**Author:** Alvin Janton  
**Email:** alvinjanton575@gmail.com

---

## Access S3 from a VPC

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-networks-s3_3e1e79a2)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service that allows you to create a virtual private cloud network. It is useful because of its cost, its ease of use, and its scalability.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create my own virtual private cloud network.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how easy this project would be.

### This project took me...

This project took me 20 minutes to do.

---

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I will launch an EC2 instance from my VPC subnet.

### Step 2 - Connect to my EC2 instance

In this step, I will connect to my EC2 instance using EC2 Instance Connect

### Step 3 - Set up access keys

In this step, I will create access keys to give my EC2 instance access to my account.

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

Access keys are similar to a username and password, they allow for access to your an AWS user to an external host.

Secret access keys are passwords created by AWS that you can use to configure access to your AWS account.

### Best practice

Although I'm using access keys in this project, a best practice alternative is to use AWS CLI V2 and enable authentication through an IAM user.

---

## In the second part of my project...

### Step 4 - Set up an S3 bucket

In this step, I will create an S3 bucket.

### Step 5 - Connecting to my S3 bucket

In this step, I will try to connect my EC2 instance to my S3 bucket.

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

---
