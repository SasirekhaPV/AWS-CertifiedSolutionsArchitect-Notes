# SECTION 3 | IAM AND S3

## S3

### What is S3?

- One of the oldest AWS services 
- Makes up a lot of the AWS exam
- Stands for 'Simple Storage Service'
- Provides devs and IT teams with secure, durable, highly-scalable object storage
- It's easy to use, with a simple web services interface to store and retrieve any amount of data from anywhere on the web

### What does S3 do? 

- It's a safe place to store your files e.g. word documents, pictures, media
- Object-based storage
- Data is spread across multiple devices and facilities

### Basics of S3

- Object-based - i.e. allows you to upload files
- By default, all newly created buckets are PRIVATE. You can setup access control to your buckets using 1. bucket policies and 2. access control lists 
- S3 buckets can be configured to create access logs which log all requests made to the S3 bucket. This can be sent to another bucket and even another bucket in another account. 
- Files can be from 0 bytes to 5 TB
- There is unliimited storage
- Files are stored in buckets
- A bucket is just a term for a public cloud storage resource - almost like a file
- S3 is a universal namespace. That is, names must be unique globally. It includes the location of the region as well e.g. https://s3-eu-west-1.amazonaws.com/acloudguru
- When you upload a file to S3, you will receive a HTTP 200 code (popular exam question)

### Objects

- Key (name of the object)
- Value (simply the data and is just made of up a sequence of bytes)
- Version ID (important for versioning) - can access all versions of an object on S3
- Metadata (Data about data you are storing)
- Subresources - access control lists and torrent

### How does data consistency work for S3? 

- Read after write consistency for PUTS of new objects. This means that if you upload a file to S3, you are able to read it immediately straight after writing it. You are putting a 'put' of that object onto S3
- Eventual consistency for overwrite PUTS and DELETES (can take some time to propogate) - if you immediately try and read the object, basically you may get V2 or V1, for example. If you wait a few moments, you will get V2 i.e. eventually it will become consistent

### S3 Gaurantees

- Built for 99.99% available for the S3 platform
- Amazon Guarantee 99.99% availability
- Amazon guarantees 99.99999999999% (11 nines) durability for S3 information - this means that in the small amount of cases (very minimal) - data may be lost.  

### S3 has the following features (fundamental to the exam)

- Tiered storage available
- Lifecycle management e.g. when this file is 30 days old move it to a certain tier or archive it
- Versioning - multiple versions of objects in an S3 bucket
- Encryption - different encryption mechanisms
- MFA Delete - when you turn this on, if someone goes to delete this, they will need multi factor authentication 
- Secure your data using Access Control Lists and Bucket Policies

### S3 Storage Classes

1. S3 standard: Has 99.99% availability and 99.99999999999% durability stored redundantly accross multiple facilities, and is designed to sustain the loss of 2 facilities concurrently. 
2. S3-IA (infrequently accessed): For data that is accessed less frequently, but requires rapid access when needed. Lower fee than S3, but you are charged a retrieval fee.
3. S3 One Zone - IA (used to be called reduced redundancy storage or RRS): For where you want a lower-cost option for infrequently accessed data, but do not require the multiple Availability Zone data resilience.
4. S3 - Intelligent Tiering - Designed to optimise costs by automatically moving data to the most cost-effective access tier, without performance impact or operational overhead.
5. S3 Glacier - Secure, durable and low-cost storage class for data archiving. You can reliably store any amount of data at costs that are competitive with or cheaper than on-premises solutions. Retrieval times configurable from minutes to hours. 
6. S3 Glacier Deep Archive - S3 Glacier Deep Archive is Amazon S3's lowest-cost storage class where a retrieval time of 12 hours is acceptable. If you want data back, you have to put in a request. Need to remember this for exam!

### S3 - Charges

You are charged in the following ways:
- Storage
- Requests
- Storage Management Pricing
- Data Transfer Pricing
- Transfer Acceleration (Enables fast, easy and secure transfer of files over long distances between your end users and an S3 bucket. Transfer Acceleration takes advantage of Amazon CloudFront's globally distributed edge locations. As the data arrives at an edge location, data is routed to Amazon S3 over an optimised network path)
- Cross Region Replication (When you want to replicate an object from Region A to Region B for disastor recovery or high availability reasons)

### Encryption (important)

- Encryption In Transit is achieved by: 
1. SSL/TLS - that's when you are browsing using HTTPS
Encryption At Rest (Server Side) is achieved by:
1. S3 managed keys - SSE-S3 - Amazon manages this for you with their keys e.g. AES-256
2. AWS key management service - this is where you and Amazon manage the keys together - SSE-KMS (more beyond the scope of the course - covered in the Security Course)
3. Server side encryption with customer provided keys (where you give Amazon your own keys that you manage) - SSE-C
Client Side Encryption
- Encrypting on your Mac or PC and then you upload

### Versioning with S3

- Stores all versions of an object (including all writes even if you delete an object)
- Great backup tool
- Once enabled, versioning CANNOT be disabled, it can only suspended
- Integrates with lifecycle rules
- Comes with MFA Delete capabilities to provide additional layer of security. Uses multi factor authentication to prevent people from accidentally deleting objects. 
- Remember that each version you upload will increase your data usage as a result of versioning

### S3 Transfer Acceleration

- Utilises the CloudFront Edge Network to accelerate your uploads to S3. Instead of uploading directly to your S3 bucket, you can use a distinct URL to upload directly to an edge location which will then transfer that file to S3. You will then get a distinct URL to upload to. 

### CloudFront

- A Content Delivery Network (CDN) is a system of distributed servers (network) that deliver webpages and other web content to a user based on the geographic locations of the user, the origin of the webpage, and a content delivery server
- E.g. if a website is hosted in London. When a user goes to the website - they will go to London and pull that content down, literally, across oceans. 
- Edge Location - The location where the content will be cached. This is separate to an AWS region/AZ
- Origin. The origin of all the files that the CDN will distribute. This can be an S3 bucket, an EC2 instance, an Elastic Load Balancer, or Route53
- Distribution. This is the name given to the CDN which consists of a collection of Edge Locations
- Can be used to deliver entire website, including, dynamic, static, streaming and interactive content using a global network of EL. Requests for your content are automatically routed to the nearest EL, so content is delivered with the best possible performance.

There are two types of distribution:

Weeb Distribution - typically used for websites
RTMP - used for media streaming

### Snowball

- A petabyte-scale data transport solution (big disc) that uses secure appliances to transfer large amounts of data into and out of AWS
- Using snowball addresses common challenges with large-scale data transfers including high network costs, long transfer times, and security concerns. Transferring data with Snowball is simple, fast, secure, and can be as little as one-fifth of the cost of high-speed internet
- Two flavours - 50TB or 80TB
- Uses multiple layers of security designed to protect data including tamper resistant enclosures, 256-bit encryption, and an industry-standard Trusted Platform Module (TPM) diesgned to ensure both security and full chain-of-custody of your data. Once the data transfer job has been processed and verified, AWS performs a software erasure of the Snowball appliance
- Snowball Edge: 100TB of data with on-board storage and compute capabilities. You can use Snowball Edge to move large amounts of data into and out of AWS, as a temporary storage tier for large local datasets, or to support local workloads in remote or offline locations
- Can cluster together to form a local storage tier and process your data on-premises, helping ensure your applications continue to run even when they are not able to accecss the cloud. Sort of like having a portable version of AWS
- AWS Snowmobile is an exabyte-scale data transfer service used to move extremely large amounts of data to AWS. You can transfer up to 100PB per Snowmobile, a 45-foot long shipping container, pulled by a truck. Makes it easy to move massive volumes of data to the cloud, including video libraries, image repos, or even a complete data center migration. Transferring data with Snowmobile is secure, fast and cost effective
- Can import to S3 and export from S3

### Storage Gateway

- Storage Gateway is a service that connects an on-premises software appliance with cloud-based storage to provide seamless and secure integration between an organisation's on-premesis IT environment and AWS's storage infrastructure. Enables secure storage of data to the AWS Cloud for scalable and cost-effective storage
- Available to download as a virtual machine (VM) image that you instlal on a host in your datacenter. 
- Supports Hyper-V or VMware ESXi
- You can use AWS Management Console to create storage option that is right for you 
- Comes in 3 flavours
	1. File gateway (NFS & SMB)
	2. Volume Gateway (iSCSI)
		- Stored volumes
		- Cached volumes
	3. Tape Gateway (virtual tape library)
- Files are stored as objects in your S3 buckets, accessed through an NFS mount point. Once objects are transferred to S3, they can be managed as native S3 objects. Basically a way of connecting your on-premise infrastructure
- Volume gateway presents your paplications with disk volumes using iSCSI block protocol. Can be async backed up as point-in-time snapshots of your volumes, and stored in the cloud as Amazon EBS snapshots
- They are incremental backups that capture only changed blocks. All snapshot storage is also compressed to minimise your storage charges
- Stored volumes let you store your primary data locally, while async backing up that data to AWS. Provide your on-premises applications with low-latency access to their entire datasets, while providing durable, off-site backups. Can create storage volumes and mount them to iSCSI devices from your on-premesis storage hardware. This data is async backed up to Amazon Simple Storage Service (Amazon S3) in the form of Amazon Elastic Block Store (Amazon EBS) snapshots. 1GB - 16TB in size for Stored Volumes. 
- Cached volumes doesn't do the data set locally, only the most frequently used data set locally in  your storage gateway. Can create storage volumes of up to 32 TB in size and attach to them as iSCSI devices from your on-premises application services. Your gateway stores data that you write to these volumes in Amazon S3 and retains recently read data in your on-premeses storage gateway's cache and upload buffer storage. 1GB - 32 TB in size for cached volumes. 
- Each tape gateway is preconfigured with a media changer and tap drives, which are available to your existing client backup applications as iSCSI devices. YOu add tape cartridges as you need to archive your data. Supported by NetBackup, Backup Exec, Veeam etc.


### Exam Tips

- Remember that S3 is Object-based i.e. allows yout upload files
- Files can be from 0 bytes to 5 TB
- There is unlimited storage
- Files are stored in buckets
- S3 is a universal namespace - unique name
- Upload an object to S3 to receive a HTTP 200 code
- Storage classes: S3, S3 - IA, S3 - IA (One Zone), Glacier
- Control access to buckets using a bucket ACL or using bucket policies

As S3 is object-based, it is not suitable to install an OS or host a DB on. For this, you want block based storage. FILES ONLY. Successful uploads will generate a HTTP 200

Key fundamentals:
-Key (name of the object)
-Value (Simply the data and is made up of a sequence of bytes)
-Version ID (Important for versioning)
-Metadata (Data about data you are storing)
-Subresources - Access Control Lists and Torrent

Read after write consistency for PUTS of new objects
Eventual consistency for overwrite PUTS and DELETES (can take some time to propogate)
Read the S3 FAQs before the exam

Versioning
- Stores all versions of an object (including all writes and even if you delete an object)
- Great backup tool
- Once enabled, it cannot be disabled, only suspended
- Integrates with Lifecycle rules
- Versioning's MFA Delete capabilities, which uses MFA to provide extra layer of security

Lifecycle
- Automates moving objects between different storage tiers
- Can be used in conjunction with versioning
- Can be applied to current versions and previous versions as well

Cross Region Replication
- Versioning must be enabled on both the source and destination bckets
- Regions must be unique
- Files in an existing bucket are not replicated automatically
- All subsequent updated files will be replicated automatically
- Delete markers are not replicated

CloudFront
- Edge location - this is the location where the content will be cached. This is separate to an AWS Region/AZ
- Origin - this is the origin of all the files that the CDN will distribute. This can either be an S3 Bucket, an EC2 Instance, an Elastic Load Balancer or Route53
- Distribution - this is the name given to the CDN which consists of a collection of EL
- Web Distribution - tyepically used for websites
- RMP - media streaming
- Objects are cached for the TTL (Time to Live)
- EL are not just read only - you can write to them too i.e. put an object to them
- You can clear cached objects, but you will be charged (e.g. if the user is downloading an old video, and you remove it and add/update new data, you will be charged)

Snowball 
- Understand what it is
- Snowball can import to S3 and export from S3

Storage Gateway
- For flat files, stored directly on S3
- Stored Volumes: Entire dataset is stored on site and is async backed up to S3
- Cached Volumes: Entire dataset is stored on S3 and the most frequently accessed data is cached on site 
- Gateway Virtual Tape Library