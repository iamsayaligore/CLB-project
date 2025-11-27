# **Deploying a Classic Load Balancer in AWS** 

## **📘 Introduction**

The *Classic Load Balancer (CLB)* is one of the earliest load balancers offered by AWS. It automatically distributes incoming application traffic across multiple EC2 instances to ensure high availability, fault tolerance, and scalability.

In this guide, you’ll learn how to set up and configure a Classic Load Balancer step-by-step using the AWS Management Console.


## **🧩 Prerequisites**


Before starting, make sure you have:

• An active *AWS account*

• At least *two EC2 instances* running in the same region

• A configured *Security Group* that allows HTTP (port 80) or HTTPS (port 443) traffic

• Basic understanding of *VPC, **subnets, and **EC2*


## **⚙ Steps to Deploy Classic Load Balancer**

### **Step 1: Login to AWS Management Console**

1. Go to [https://aws.amazon.com/console/](https://aws.amazon.com/console/).


### **Step-1 Launch EC2 Instances**

• Launch three sets of EC2 instances (Server-A,Server-B,server-c), with two instances in each set.

• Select security group.

• choose t2.micro (Free Tier).

![alt text](<Screenshot 2025-09-29 224323.png>)


### **Step 2: Open the Load Balancer Section**
1. In the *EC2 Dashboard, scroll down and select **Load Balancers* under the *Load Balancing* section.
2. Click on *Create Load Balancer*.

![alt text](<Screenshot 2025-09-29 224401.png>)

### **Step-3. Add user Data Script (For each instance)**

Add the following script in user data lunching home instance:
     
       #!/bin/bash
       yum update -y 
       yum install httpd -y 
       systemctl start httpd 
       systemctl enable httpd 
       echo "<h1>This is home page $(hostname -f)</h1>" > /var/www/html/index.html


### **Step 4: Select Classic Load Balancer**
1. Choose *Classic Load Balancer* from the available options.
2. Click *Create*.

![alt text](<Screenshot 2025-09-29 224505.png>)


### **Step 5: Configure Load Balancer**
1. *Name* your load balancer.

![alt text](<Screenshot 2025-09-29 232026.png>)

2. Choose the *scheme*:
   - *Internet-facing* (for public access)
   - *Internal* (for internal network only)

![alt text](image.png)

3. Select the *Network (VPC)* and *Availability Zones* where your EC2 instances are running.

![alt text](<Screenshot 2025-09-29 232054.png>)


### **Step 6: Add EC2 Instances**
1. Select the instances you want to register with the load balancer.
2. Click *Add to Registered*.

![alt text](<Screenshot 2025-09-29 232425.png>)


### **Step 7: Review and Create**
1. Review all configurations.
2. Click *Create* to launch the Classic Load Balancer.
3. Wait until the status becomes *Active*.

![alt text](<Screenshot 2025-09-29 232613.png>)


### **✅ Verification**

- Go to the *Description tab* of your load balancer.
- Copy the *DNS name* 
- Paste it in your browser — it should load your application served by one of the EC2 instances.


![alt text](<Screenshot 2025-09-29 232922.png>)

![alt text](<Screenshot 2025-09-29 232943.png>)

![alt text](<Screenshot 2025-09-29 232943-1.png>)


## **🧠 Notes**

- CLB supports both *Layer 4 (TCP)* and *Layer 7 (HTTP/HTTPS)* traffic.
- AWS recommends using *Application Load Balancer (ALB)* or *Network Load Balancer (NLB)* for new applications.
- CLB does not support advanced routing or container-based workloads.


## **🧹 Cleanup**

To avoid extra costs:
1. Deregister EC2 instances from the CLB.
2. Delete the Classic Load Balancer from the console.


## **📄 Summary**

By following this guide, you’ve successfully deployed a *Classic Load Balancer* that distributes incoming traffic evenly across EC2 instances, improving fault tolerance and availability for your AWS-hosted applica




