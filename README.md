# Devops-Interview-Questions
1.I have a private subnet and i am not attaching NAT gateway, can we call a subnet without NAT gateway as private subnet?

ANS: yes, we can call a subnet without NAT gateway as private subnet because even if we assign NAT gateway or not that is a private subnet only.if we assign NAT gateway then it means we are enabling the outbound rule to the private subnet, if does not assign that subnet will be completely isolated.

2. Explain the s3 lifecycle.
ANS: 
3. Explain the types of rules of autoscalling groups.

4. I have two or more VPC's in different AWS accounts, how can you establish the communication between the VPC's?

5. My server is in Private subnet and its has no NAT gateway attached to it and should not attach any NAT gate way. how can you access the objects inside the S3 buckets?

6. In s3 I have few private objects and I want to give access to a user for just 10 minutes. how will you do that without using creting roles?

7. In cloud i need few database servers to be create everyday at a prticular time(9AM) and deleted in the evening(6PM) to reduce the billing how can you do that?
