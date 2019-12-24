# SECTION 10 | Serverless

## Lambda

- Data Centres
- Hardware
- Assembly Code/Protocols
- High Level Languages
- Operating Systems
- Application Layer/AWS APIs
- AWS Lambda

## What is Lambda?

- Compute service where you can upload your code and create a lambda function. It takes care of provisioning and managing the servers that you use to run the code. You don't have to worry about operating systes, patching, scaling etc.
- You can use it as an event-driven compute service where AWS Lambda runs your code in response to events. These events could be changes to data in an Amazon S3 bucket or an Amazon Dynamo DB table
- You could also use it as a compute service to run your code in response to HTTP requests using Amazon API Gateway or API calls made using AWS SDK
- User wants to create meme -> uploads to an S3 bucket -> lambda function will take that meme and caption it over the meme 
- Lambda functions can trigger other lambda functions or it could store that meme somewhere else in the world using cross region replication 
- Supports Go, Node.js, Java, Pythom, C#, Go, PowerShell
- No patching your OS, no need to worry anti virus or servers or SysAdmins
- Continuous Scaling 
- Very cheap 

## Traditional vs Serverless Architecture 

- Traditional: User sends requests -> hits R53 -> hits LB -> web servers may communicate with backend and then sends back a response to the user
- Serverless: Reponse to API gateway -> response to Lambda -> can write to DynamoDB and then it will send a response back to the user 
- In the exam, you will have scenario questions and they will test you on serverless architecture

## Pricing

- First one million requests are free and $0.20 per million requests thereafter
- Duration: calculated from the time your code begins executing until it returns or otherwise terminates, rounded up to the nearest 100ms. The price depends on the amount of memory you allocate to your function. You are charged for $0.00001667 for every GB-second used

## Lambda Exam Tips

- Scales out automatically 
- Lambda functions are independent, 1 event = 1 function
- Know what services are severless! 
	RDS is not serverless. Aurora serverless is the only thing IS serverless
	DynamoDB, S3, API Gateway are all serverless
	EC2 IS NOT serverless - it's a virtual machine
- Lambda functions can trigger other functions
- AWS X-ray allows you to debug 
- Know your triggers - know what can't trigger Lambda
- Lambda can do things globally, you can use it to back up S3 buckets to toher S3 buckets etc. 


