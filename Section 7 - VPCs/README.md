# SECTION 7 | VPCs

- A VPC is your private section fo AWS, where you can place AWS resources, and allow or restrict access to them 
- 

## Reserved IP Addresses

- 10.0.0.0 - Network Address
- 10.0.0.1 - Reserved by AWS for the VPC Router
- 10.0.0.2 - Reserved by AWS for the DNS server
- 10.0.0.3 - Reserved for future reasons
- 10.0.0.255 - Network broadcast
- This is why it normally states that there are 251 available addresses instead of 255. 

## NAT Instances

- Know the difference between NAT instance and NAT Gateway for the exam 
- NAT instance is just an EC2 instance
- NAT gateway is a highly available gateway that allows you to have your private subnets communicate out to the internet without becoming public 


## Internet Gateway 

- You can only have one Internet Gateway per VPC
- Allows communication between instances in your VPC and the internet

## Exam Tips

- When you create a VPC, a default Route Table, Network Access Control List (NACL) and a default Security Group
- It won't create any subnets, nor will it create a default internet gateway
- US-East-1A in your AWS account can be completely different AZ to US-East-1A in another AWS account. The AZ's are randomised
- Amazon reserve 5 IP addresses within your subnets
- You can only have 1 Internet Gateway per VPC
- Security can't span VPCs