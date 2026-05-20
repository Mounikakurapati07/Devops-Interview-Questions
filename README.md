# Devops-Interview-Questions
1.I have a private subnet and i am not attaching NAT gateway, can we call a subnet without NAT gateway as private subnet?                                                                   
ANS: yes, we can call a subnet without NAT gateway as private subnet because even if we assign NAT gateway or not that is a private subnet only.if we assign NAT gateway then it means we are enabling the outbound      rule to the private subnet, if does not assign that subnet will be completely isolated.

2. Explain the s3 lifecycle.
ANS: S3 Lifecycle helps you store objects cost effectively throughout their lifecycle by transitioning them to lower-cost storage classes, or, deleting expired objects on your behalf. To manage the lifecycle of your objects, create an S3 Lifecycle configuration for your bucket. An S3 Lifecycle configuration is a set of rules that define actions that Amazon S3 applies to a group of objects. There are two types of actions:
Transition actions – These actions define when objects transition to another storage class.                                                    
Expiration actions – These actions define when objects expire. Amazon S3 deletes expired objects on your behalf. 
4. Explain the types of rules of autoscalling groups.                                                                                                               ANS: there are different types of rules in autoscalling.
       1.Simple scalling:The most basic type.Uses CloudWatch alarms to trigger scaling actions.When the alarm is breached, ASG performs a single scaling action           (add/remove instances).After scaling, a cooldown period is applied before another action occurs.
       Example:
       If CPU > 70% → Add 1 instance
       If CPU < 30% → Remove 1 instance
       2. Stepscalling
       3. treget tracking scalling
       4. scheduled scalling
       5. predictive scalling

6. I have two or more VPC's in different AWS accounts, how can you establish the communication between the VPC's?

7. My server is in Private subnet and its has no NAT gateway attached to it and should not attach any NAT gate way. how can you access the objects inside the S3 buckets?

8. In s3 I have few private objects and I want to give access to a user for just 10 minutes. how will you do that without using creting roles?
   ANS: You can do this easily using an S3 Pre-Signed URL.This allows temporary access (like 10 minutes) to a private S3 object without creating roles, users, or policies.
     we can do this in multiple ways like using AWS CLI, or by writing Python script, or by writing terraform script and also we can create manually.
     aws s3 presign s3://mybucket/myobject.txt --expires-in 600 (AWS CLI way of creating URL)  we can give this URL so that they can access the s3 objects till that time expires.

9. In cloud i need few database servers to be create everyday at a prticular time(9AM) and deleted in the evening(6PM) to reduce the billing how can you do that?                                                    
ANS: You can automate this easily in AWS using EventBridge + Lambda (or Systems Manager Automation).
     This approach lets you create DB servers at 9 AM and delete them at 6 PM, reducing cost with zero manual work.
     9 AM → EventBridge rule triggers a Lambda → Lambda creates your DB servers.
     6 PM → Another EventBridge rule triggers another Lambda → Lambda deletes them.
     Works with:
     EC2 database servers (MySQL/PostgreSQL running on EC2)
     RDS Instances
     DocumentDB
    Any custom DB server                                                                                                                                                     

10. Difference between ingress and Load balancer?                                                                                                                                              

11. what is headless service?                                                                                                                                        
ANS: A Headless Service in Kubernetes is a type of Service that does not provide a ClusterIP. Instead of load-balancing traffic, it allows clients to directly discover and connect to individual Pods.
    spec:
       clusterIP: None
    Headless services are used for apps that need to handle load balancing themselves — e.g., Stateful apps like databases.

12. Can you attach a single EBS volume to multiple EC2 instances at the same time?

ANS:    No, you cannot attach a single Amazon EBS (Elastic Block Store) volume to multiple EC2 instances at the same time in the traditional way. An EBS volume is designed to be attached to only one EC2 instance at a time, and it behaves like a block device. If you try to attach it to multiple instances simultaneously, you risk data corruption because block storage doesn’t handle concurrent writes safely across multiple servers.

Alternatives
Amazon EFS (Elastic File System): If you need shared storage accessible by multiple EC2 instances at the same time, EFS is the right choice. It provides a scalable, managed NFS file system that multiple instances can mount concurrently.

Amazon FSx: For workloads requiring Windows File Server or Lustre, FSx provides shared file storage.

Clustered File Systems on EBS: In advanced setups, you can technically attach an EBS volume to multiple instances in read-only mode, or use specialized clustered file systems (like GFS2 or OCFS2) with careful configuration. But this is complex and not the default or recommended approach.

So, the short answer: No, not directly. Use EFS or FSx if you need shared storage across multiple EC2 instances.

12. Difference between security groups and NACL

13. I have an image and container is running with that image.Can you able to delete that image? and what happens if you delete that image?                                                                 

14. How can we maintain the different version a file in git?                                                                                                 

https://medium.com/@chandrashekhar.cr/top-10-aws-scenario-based-interview-questions-and-answers-2025-5ddcd5404bb7
https://www.linkedin.com/posts/ops-mohammed-irfan-shaikh_kubernetes-cloudnative-devops-activity-7414266741918441473-Kxxz?utm_source=social_share_send&utm_medium=android_app&rcm=ACoAADhRbxoBAheuPuDQcKkXqDpp84EuggQouWw&utm_campaign=whatsapp

15. Can we able to attach the AMI directly as base image in docker file?

16. i have three apllications like amazon, flipcard, mintra each application need 40GB volume but you have only 100 GB volume how can you assign the volume to all the three applications.

17. i have one application which is hosted in my ec2 instace which is present in a private subnet and from google i am requestig to access it, can you walk us which AWS services will include in the process of reaching my application request from browser to application.

18. How to access the S3 bucket privately?
ANS: To access an Amazon S3 bucket privately, you need to ensure that traffic between your applications and S3 stays within the AWS network, without going through the public internet. Here are the main approaches:

a. Use VPC Gateway Endpoints
Create a VPC endpoint for S3 in your Virtual Private Cloud (VPC).
This allows EC2 instances in private subnets to access S3 directly, without requiring an internet gateway or NAT device.
Traffic remains inside the AWS backbone network, improving security and reducing costs.
b.. Restrict Bucket Access with IAM Policies
Configure bucket policies to allow access only from specific VPC endpoints or IAM roles.
This ensures that only authorized users or applications can interact with the bucket.
c. Private Access via Presigned URLs
Generate presigned URLs that grant temporary, controlled access to specific objects in the bucket.
Combine this with VPC endpoints to ensure the access happens only within your private network.
d. Block Public Access
Enable Block Public Access settings on the bucket to prevent accidental exposure.
This ensures no object or bucket can be made publicly accessible.
e. Encryption and Access Control
Use S3 server-side encryption (SSE) or KMS-managed keys for data protection.
Apply fine-grained IAM permissions to control who can read/write objects.

19. How many VPC's we can create in a region?
ANS: By default, you can create up to 5 VPCs per AWS Region in your account. However, this quota is adjustable — you can request an increase through the AWS Service Quotas console or by contacting AWS Support.
With an approved quota increase, it’s possible to have hundreds of VPCs per Region if your architecture requires it.
Scalability: Can be increased to hundreds per Region if needed.
Quick Summary
Default limit: 5 VPCs per Region.
Adjustable: Yes, via Service Quotas or AWS Support.

20. Production EKS app went down at 2 AM. What is your immediate action plan?
ANS: “First, I acknowledge the alert and assess blast radius using monitoring dashboards. I check Kubernetes pod, node and event status to identify if it’s application, cluster or infra related. I quickly review recent deployments and logs.
If the outage is caused by a bad deployment, I immediately roll back. If pods are crashing due to resource or node issues, I scale replicas or replace unhealthy nodes.
While fixing, I keep stakeholders informed every 10–15 minutes.
After restoration, I validate service health, monitor stability and later perform RCA with preventive measures like better alerts, probes and autoscaling.”

21.Pods are in CrashLoopBackOff after deployment. How will you troubleshoot?
ANS:“First I confirm if only the new deployment pods are crashing. I describe the pod and check previous container logs to identify the failure reason. I compare the new deployment with the last working revision to see what changed — image, config, secrets or resource limits.
To restore production fast, I immediately roll back the deployment. After service is stable, I fix the root cause and add preventive measures like canary deployments, better probes and CI validation.”

RETHINK PASSION INTERVIEW QUESTIONS
-----------------------------------

1. linux command to copy files from one server to another
2. command to check drive details
3. command to check ports --->
4. linux command to create a soft link to a file
5. how will you download a folder from s3 buckets
6. how will you recover the currepted EBS volume of an instance 
7. I have one ec2 instance and how will you create the EC2 instance with same configrations like existing ec2 instance
8. difference between copy and ADD in docker file
9. explain why do you use docker compose
10. explain about the concept of CloudFront 
11. what do you know about the RDS and whave you ever worked on it?


Qvantel Interview questions
-----------------------------
1. explain clearly how you will you access the files in s3 from a server in Private subnet.
2. difference between ALB and NLB
3. demonstrate the CI/CD pipeline how you will zip the files from a github and upload them in S3
4. what are the types of IAM policies
5. did you ever work on creating the transition gateway and side to side gateway
6. how will you create a application load balancer in Terraform
7. explain me in terraform perspective how you wil create the VPC
8. difference between the systems manager and secrets manager
9. how you will store and access the credentials from AWs secrets manager
10. what are the types of storages that you worked on (ex: block storage, filestorage)
11. explain how you will attach the block storage to a ec2 instance
12. what are primary and sencondary storages paths(/XUV
13. 


    
