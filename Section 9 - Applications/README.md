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