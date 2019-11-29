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
- Files can be from 0 bytes to 5 TB
- There is unliimited storage
- Files are stored in buckets
- A bucket is just a term for a public cloud storage resource - almost like a file
- S3 is a universal namespace. That is, names must be unique globally. It includes the location of the region as well e.g. https://s3-eu-west-1.amazonaws.com/acloudguru
- When you upload a file to S3, youw ill receive a HTTP 200 code (popular exam question)

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
