# Devops-Interview-Questions
1.I have a private subnet and i am not attaching NAT gateway, can we call a subnet without NAT gateway as private subnet?                                                                   
ANS: yes, we can call a subnet without NAT gateway as private subnet because even if we assign NAT gateway or not that is a private subnet only.if we assign NAT gateway then it means we are enabling the outbound rule to the private subnet, if does not assign that subnet will be completely isolated.

2. Explain the s3 lifecycle.
ANS: 
3. Explain the types of rules of autoscalling groups.                                                                                                                 

4. I have two or more VPC's in different AWS accounts, how can you establish the communication between the VPC's?

5. My server is in Private subnet and its has no NAT gateway attached to it and should not attach any NAT gate way. how can you access the objects inside the S3 buckets?

6. In s3 I have few private objects and I want to give access to a user for just 10 minutes. how will you do that without using creting roles?                                                                     ANS: You can do this easily using an S3 Pre-Signed URL.This allows temporary access (like 10 minutes) to a private S3 object without creating roles, users, or policies.
     we can do this in multiple ways like using AWS CLI, or by writing Python script, or by writing terraform script and also we can create manually.
     aws s3 presign s3://mybucket/myobject.txt --expires-in 600 (AWS CLI way of creating URL)  we can give this URL so that they can access the s3 objects till that time expires.

7. In cloud i need few database servers to be create everyday at a prticular time(9AM) and deleted in the evening(6PM) to reduce the billing how can you do that?                                                    
ANS: You can automate this easily in AWS using EventBridge + Lambda (or Systems Manager Automation).
     This approach lets you create DB servers at 9 AM and delete them at 6 PM, reducing cost with zero manual work.
     9 AM → EventBridge rule triggers a Lambda → Lambda creates your DB servers.
     6 PM → Another EventBridge rule triggers another Lambda → Lambda deletes them.
     Works with:
     EC2 database servers (MySQL/PostgreSQL running on EC2)
     RDS Instances
     DocumentDB
    Any custom DB server                                                                                                                                                     
8. Difference between ingress and Load balancer?                                                                                                                                              
9. what is headless service?                                                                                                                                        
ANS: A Headless Service in Kubernetes is a type of Service that does not provide a ClusterIP. Instead of load-balancing traffic, it allows clients to directly discover and connect to individual Pods.
spec:
  clusterIP: None
Headless services are used for apps that need to handle load balancing themselves — e.g., Stateful apps like databases.
10. Difference between security groups and NACL
11. I have an image and container is running with that image.Can you able to delete that image? and what happens if you delete that image?                                                                 
12. How can we maintain the different version a file in git?                                                                                                 

