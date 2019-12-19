# SECTION 3 | EC2

## What is EC2?

- Web service that provides resizable compute capacity in the cloud. Reduces the time required to obtain and boot new server instances in minutes, allowing you to quickly scale capacity, both up and down, as your computing requirements change

## Pricing Models

1. On Demand: Allows you to pay a fixed rate by the hour (or by the second) with no commitment

	- Users that want low cost and flexibility of Amazon EC2 without any up-front payment or long-term commitment
	- Applications with short term, spiky, or predictable workloads that cannot be interrupted
	- Applications being developed or tested on EC2 for the first time

2. Reserved: Capacity reservation, and offer a significant discount on the hourly charge for an instance. Contract terms are 1 or 3 year terms. More you pay upfront, the more discount you get

	- Applications with steady state or predictable usage
	- Applications that required reserved capacity
	- Users able to make upfront payments to reduce their total computing costs even further
	- Several types: Standard reserved instances (offer up to 75% on demand instances); Convertible reserved instances (offer upt o 54% off on demand capability); Scheduled reserved instances (are available to launch within the time windows you want to reserve. Allows you to match your capacity reservation to a predictable recurring schedule that only requires a fraction of a day, a week, or a month)

3. Spot: Enables you to bid whatever price you want for instance capacity, providing for even greater savings if your applicaitons have flexible start and end times. 

	- Applications that have flexible start and end times
	- Applications that are only feasible at very low compute prices
	- Users with urgent computing needs for large amounts of additional capacity

4. Dedicated Hosts: Physical EC2 server dedicated for your use. Can help reduce costs by allowing you to use existing software-bound licenses

	- Regulatory requirements that may not support multi-tenant virtualisation 
	- Great for licensing that doesn't support multi-tenancy or cloud deployments 
	- Can be purchased On-Demand
	- Can be purchased as a reservation for up to 70% off the demand price


## Security Groups 

## EBS 101

- Provides persistent block storage
- Virtual disc storage for the coud
- Each Amazon EBS volume is automatically replicated within its AZ to protect you from component failure, offering high availability and durability
- Offers high durability and availability

5 different types:
	1. General purpose (SSD) - gp2
	2. Provisioned IOPS (SSD) - io1
	3. Throughput Optimised Hard Disk Drive - st1
		Used for big data or data warehousing
	4. Cold Hard Disk Drive - sc1
		Lowest cost hard disc drive and designed for less frequently accessed workloads such as file servers
	5. Magnetic - Standard
		Previous generation hard disk drive - still available though
		For workloads where data is infrequently accessed and you may choose not to use Glacier

A Snapshot is the photograph of the disk. It takes a bit of time to create. If you are creating an image, and you want as many different EC2 instance types, you want virtualisation on hardware-assisted virtualisation. This will give you a lot omre EC2 instance types later on. You can copy AMIs and then migrate them across AZ's. 

## AMI Types (EBS vs Instance Store)

- You can select AMI based on:
	1. Region 
	2. OS
	3. Architecture (32 or 64 bit)
	4. Launch permissions
	5. Storage for the root device (root device volume)
		Instance store (ephemeral storage)
		EBS Backed volumes

- All AMIs are categorised as either backed by Amazon EBS or backed by instance store
- For EBS Volumes: The root device for an instance launched from the AMIs is an Amazon EBS volume created by an Amazon EBS snapshot
- For Instance Store Volumes: The root device for an instance launched from the AMI is an instance store volume created from a template stored in Amazon S3
- Instance Store Volumes are sometimes called Ephemeral Storage. If some reason they stop - you will lose all your data
- Instance store volumes cannot be stopped. If the underlying host fails, you will lose your data
- EBS backed instances can be stopped. You will not lose the data on this instance if it is stopped. 
- You can reboot both, you will not lose your data. 

By default, both ROOT volumes will be deleted on termination. However, with EBS volumes, you can tell AWS to keep the root device volume.

## Encrypted Root Device Volumes & Snapshots

- Launch encrypted root device volume to encrypt an unencrypted device
- Snapshots of encrypted volumes are encrypted automatically
- Volumes restored from encrypted snapshots are encrypted automatically
- You can share snapshots, only if they are unecrypted
- These snapshots can be shared with other AWS accounts or be made public
- You can now encrypt root device volumes upon creation of the EC2 instance
- Create a Snapshot of the unecrypted root device volume
- Create a copy of the Snapshot and select the encrypt option 
- Create an AMI from the encrypted Snapshot
- Use that AMI to launch new encrypted instances

## CloudWatch 101 

- Note: usually worth 3-4 marks in the exam
- Monitors performance such as 
	Compute
	Autoscaling Groups
	Elastic Load Balancers
	Route53 Health Checks
- Storage and content delivery
	EBS volumes
	Storage gateways
	CloudFront
- Host Level Metrics consists of:
	CPU
	Network
	Disk
	Status check - underlying hypervisor and underlying EC2 instance

AWS CloudTrail increases visibility into your user and resource activity by recording AWS Management Console actions and API calls. You can identify which users and accounts were called AWS, the source IP address from which the calls were made, and when the calls occurred. It is like a CCTV camera

## Exam Tips

- EC2 is a web service that provides resizable computer capacity in the cloud
- Reduces the time to obtain and boot new server instances to minutes, allowing you to quickly scale capacity, both up and down, as your computing requirements change
- Remember the different pricing types
	1. On demand
	2. Reserved
	3. Spot
		- If the Spot instance is terminated by EC2, you will not be charged for a partial hour of usage. If you terminate the instance yourself, you will be charged for any hour in which the instance ran.
	4. Dedicated hosts

- EC2 Instance Types

- You can encrypt root device volumes (very popular exam topic)
- Termination protection is turned off by default, so you must turn it on. Once you turn it off, you have to turn it off again
- On an EBS-backed instance, the default action is for the root EBS volume to be deleted when the instance is terminated
- EBS root volumes of your default AMI's can be encrypted. You can also use a third party tool such as bit locker to encrypt hte root volume, or this can be done when creating AMI's in the AWS console or using the API
- Whereever your EC2 instance is, the EBS volume will be in the same availability zone. 

EBS
- Volumes exist on EBS. Think of EBS as a virtual hard disk
- Snapshots exist on S3. Think of snapshots as a photograph of the disk
- Snapeshots are also incremental - this means that only blocks that have changed since your last snapshot are moved to S3
- If it's your first snapshot, it may take some time
- To create snapshot for Amazon EBS volumes that serve as root devices, you should stop the instance before taking the snapshot
- However, you can take a snap whilst the instance is running
- You can create AMI's from Volumes and Snapshots
- You can change EBS volume sizes on the fly, including changing the size and volume type
- Volumes will ALWAYS be in the same AZ AS THE EC2 instance 
- You can migrate EC2 volume from one AZ to another. Take snapshot, create AMI and then use AMI to launch EC2 to new AZ
- To move an EC2 volume from one region to another, take snapshot, create an AMI from the snapshot and then copy AMI from one region to another. Then use copied AMI to launch the new EC2 instance in the new region. 

Encryption 
- These snapshots can be shared with other AWS accounts or be made public
- You can now encrypt root device volumes upon creation of the EC2 instance
- Create a Snapshot of the unecrypted root device volume
- Create a copy of the Snapshot and select the encrypt option 
- Create an AMI from the encrypted Snapshot
- Use that AMI to launch new encrypted instances

CloudWatch
- Monitors performance
- Monitor most of AWS as well as your applications that run on AWS
- With EC2, will monitor events every 5 minutes by default
- You can have 1 minute intervals by turning on detailed monitoring
- You can create CloudWatch alarms which trigger notifications
- All about performance. CloudTrail is about auditing - COMMON EXAM QUESTION!

- Standard monitoring is 5 minutes
- Detaioed monitoring is 1 minute
- Dashboards - Creates awesome dashboards to see what is happening with your AWS environment
- Alarms - Allows you to set Alarms that notify you when particular thresholds are hit
- Events - CloudWatch Events helps you to respond to state changes in your AWS resources
- Logs - CloudWAtch Logs helps you to aggregate, monitor and store logs

