# SECTION 9 | Applications

## SQS

- Example: Travel website. User puts a query into the web server and they want to go to destination and enter a date. EC2 instance takes what user is requesting and stores in an SQS queue. We then have a fleet of EC2 web servers polling that queue and looking for that SQS message. They then query all the different airline servers and check the flight cost. They then take info and send the info back to the web server who sends it back to the user. 
- FIFO Queue are definitely ordered and you will get one time processing. THe order in which messages are sent and received is strictly preserved and a message is delivered once and remains available until a consumer processes and deletes it; duplicates are not introduced into the queue. 
- It is a web service that gives you access to a message queue that can be used to store messages while waiting for a computer to process them
- It's a distributed queue system that enables web service applicaitons to quickly and reliably queue messages that one component in the application generates to be consumed by another component. A queue is a temporary repository for messages that are awaiting processing
- Messages can contain up to 256KB of text in any format. Any component can later retrieve the messages programatically using the Amazon SQS API. 
- Queue acts as a buffer between the component producing and saving data, and the component receiving the data for processing
- Server creates message -> stored in SQS queue -> waiting for another server to process the message
- Standard queues guarantee that a message is delivered at least once. However, because of the highly-distributed architecture that allows high throughput, more than one copy of a message might be delivered out of order. They provide best effort ordering which ensures that messages are generally delivered in the same order as they are sent. It lets you have a nearly unlimited of transactions per second
- The first AWS Service and appears in exam quite regularly
- There are two types of queue: 
	- FIFO queues
	- Standard queues
- This means the queue resolves issues that arise if the producer is producing work faster than the consumer can process it, or if the producer or consumer are only intermittently connected to the network
- You can decouple the components of an application so that they run independently, easing message management between components. Any component of a distributed application can store messages in a fail-safe queue
- You can set up auto scaling and have a trigger as to how many messages are in the queue. If the messages are over an x amount, that can trigger an auto scaling event. They support message groups that allow ordered message groups within a single queue. FIFO queues are limited to 300 transactions per second (TPS), but have all the capabilities of standard queues

## Simple WorkFlow Service

- SWF is a web service that makes it easier to coordinate work across a a whole bunch of application components. It enables applications for a range of use cases, including media processing, web application back-ends, business process workflows, and analytics pipelines, to be designed as a coordination of tasks
- Tasks represents invocations of various processing steps in an application which can be performed by executable code, web service calls, human actions and scripts
- Amaazon uses it themselves inside their warehouse when they process payments and a person has to look up and pack the order
- If you have a scenario question with a human based element, you will NOT be using SQS as humans can't poll the SQS queue. Instead, you will be using SWF

## Simple Notification Service

- Web service that makes it easy to set up, operate, and send notifications from the cloud
- It provides developers with a highly scalable, flexible, and cost-effective capability to publish messages from an application and immediately deliver them to subscribers or to other applications
- Allows push notifications to Apple, Google, Fire OS and Windows Devices as well as Android Devices
- Can also deliver notifications by SMS text messages or by email to Amazon SQS or to any HTTP endpoint
- Pushes info to mobile devices
- Groups multiple recipients using topics. A topic is an access point for allowing recipients to dynamically subscribe for identical copies of the same notification. 
- When you set a billing alert for example, that's a billing topic. You can have subscribers to that topic.
- You can group together iOS, Android and SMS recipients. When you public once to a topic, SNS delivers appropriately formatted copies of your message to each subscriber
- To prevent messages being lost, all messages are published to Amazon SNS are stored redundantly across AZs

## Elastic Transcoder

- Media Transcoder in the cloud
- Convert media files from original source format into different formats that will play on smartphones, tablets, PCs, etc.
- Provides transcoding presets for popular output formats, which means that you don't need to guess about which settings work best on particular devices
- Pay based on the minutes that you transcode and the resolution at which you transcode as well
- You have an S3 Bucket -> That triggers a Lambda Function (essentially looks @ video, looks at meta data and sends to transcoder) -> Elastic Transcoder -> Stores the transcoded in another S3 Bucket

## API Gateway

- Fully managed service that makes it easy for developers to publish, maintain, monitor and secure APIs at any scale
- It's basically a doorway into your AWS environment
- You can create an API that acts as a "front door" for applications to access data, business logic, or functionality from your back-end services, such as applications running on Amazon Elastic Compute Cloud (Amazon EC2), code running on AWS Lambda, or any web application
- Basically a doorway into your AWS environment
- The users do an API call to API Gateway (front door to AWS environment) - this could be passed to Lambda, EC2 or DynamoDBZ
- It can expose HTTP endpoints to define a RESTful API
- Severless-ly connect to services like Lambda and DynamoDB
- Send each API endpoint to a different target
- Run efficiently with low cost
- Scale effortlessly
- Track and control usage by API key
- Throttle requests to prevent attacks (sometimes attackers may flood the API)
- Maintain multiple versions of API - test and dev for example

## API Gateway Configuration

- Define an API (container)
- Define Resources and nested resources (URL paths)
- For each response:
	- Select supported HTTP methods (verbs)
	- Set security
	- Choose target (such as EC2, Lambda, DynamoDB, etc.)
	- Set request and response transformations

## API Gateway Deployments

- Deploy API to a stage:
	- Use API Gateway domain by default
	- Can use custom domain
	- Now supports AWS Certificate Manager: free SSL/TLS certs

## API Gateway Caching

- Reduces the number of calls made to your endpoints and improve latency of the requests to your API
- WHen enabling caching for a stage, API Gateway caches responses from your endpoint for a specified TTL period, in seconds
- It then responds to the requests by looking up the endpoint response from the cache instead of making a request to your endpoint

## Same Origin Policy

- In computing, the same-origin policy is an important concept in the web app security model
- Under the policy, a web browser permits scripts contained in a first web page to access data in a second web page, but only if both web pages have the same origin
- This is done to prevent Cross-Sit Scripting (XSS) attacks

# Exam Tips

## SQS

- SQS is pull based not pushed based. EC2 instances are pulling the messages down from the queue. They are not pushing the messages out
- Messages are 256KB in size when you are using SQS. You can go up to 2GB but you have to go up to  S#
- Messages can be kept in the queue from 1 minute to 14 days; the default retention period is 4 days
- Visibility time out: the aount of time that the message is invisible in the SQS queue after a reader picks up that message. Provided the job is processed before the visibility time out expires, the message will then be deleted from the queue. If the job is not processed within that time, the message will become visible again and another reader will process it. This could result in the same message being delivered twice
- Visibility timeout maximum is 12 hours. The EC2 instance has this amount of time to process. 
- SQS guarantees that your messages will be processed at least once
- Amazon SQS long polling is a way to retrive messages from your Amazon SQS queues. While the regular short polling returns immediately (even if the message queue being polled is empty), long polling doesn't return a response until a message arrives in the message queue, or the long poll times out. This is a way of saving money. 

## SWF vs SQS

- SQS has a retention period of up to 14 days; with SWF, workflow executions can last up to 1 year
- Amazon SWF presents a task-oriented API, whereas Amazon SQS offers a message-oriented API
- SWF ensures that a task is assigned only once and is never duplicated. With Amazon SQS, you need to handle duplicated messages and may also need to ensure that a message is processed only once
- SWF keeps track of all the task and events in an application. With SQS, you need to implement your own application-level tracking, especially if your application uses multiple queues

## SWF Actors

- Workflow Starters - an application that can initiate or start a workflow. Could be your e-commerce website following the placement of an order, or a mobile app searching for bus times
- Deciders - Control the flow of activity tasks in a workflow execution. If something has finished (or failed) in a workflow, a Decider decides what to do next
- Activity Workers - carry out the activity tasks

## SNS Benefits

- Instantaneous, push-based delivery (NO polling)
- Simple APIs and easy integration with applications
- Flexible message delivery over multiple transport protocols
- Inexpensive, PAYG model with no up-front costs
- Web based AWS Management Console offers the simplicity of a point and click interface

## SNS vs SQS

- Both messaging systems
- SNS is push via notification or text message
- SQS polls and therefore pulls

## Elastic Transcoder

- Converts media files from their original source formats into different formats that will play on smartphones, tablets, PCs, etc. 
