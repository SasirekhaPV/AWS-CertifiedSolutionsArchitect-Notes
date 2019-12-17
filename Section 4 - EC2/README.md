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