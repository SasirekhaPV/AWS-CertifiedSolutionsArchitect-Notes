# SECTION 5 | Databases

## RDS

- Two key features: Multi-AZ for disaster recovery and read replicas for performance
- You'll likely get different scenario questions asking whether you should use Multi AZ or Read Replicas

Multi-AZ

- If you lose your primary DB, it will automatically update to the secondary DNA address
- Failover is automatic 

Read Replica

- Everytime you do a write to DB, that write is replicated (perfect copy) to another DB
- If you lose DB, there is no automatic failover. You would have to create a new URL and you have to update your EC2 instances to point to your read replica
- If you write a popular WordPress blog, and your primary DB is getting too many reads, the way to scale your DB is to have a perfect copy of it and you can point half your instances to point to your read replica and scale out this way
- You can have 5 copies of read replicas

## Difference between relation and non relational 

- Relational: You have to keep consistency accross all the records
- Non-Relational: You can have as many different columns for any given row

## Data WArehousing

- Used for business intelligence. Tools like SAP NetWeaver and SQL 
- Used to pull in very large and compelex data e.g. current performance vs. previous

## OLTP vs OLAP

- Online Transaction Processing
- If you want to find a specific order - you run a query and this will pull up a row of data. This will pull up name, address etc
- Online Analytics Processing
- If you want info about net profit, this will pull in a large number of records. It will run a whole bunch of queries in the DB
- Data Warehousing DBs use different types of architecture from a DB perspective and infrastructure layer
- AWS uses Red Shift

## ElastiCache

- Web service that makes it easy to deploy, operate and scale an in-memory cache in the cloud. This service improves the performance of web applications by allowing you to retrive information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases. 
- Uses two open-source in-memory caching engines
- A way of caching your most common web queries so when your web servers are getting a request, they will go to elasticache first and it will take a huge load off your databases 
- Consists of two different engines - Memcached and Redis

## Backups

- Two different types of backups for RDS: Automated backups and database snapshots
- Automated backups: Allow you to recover your DB to any point in time within a "retention period". The period can be between 1 to 35 days. Automated Backups take a full daily snapshot and will also store transaction logs throughout the day. When you do a recovery, AWS will first choose the most recent daily backup, and then apply transaction logs relevant to that day. This allows you to do a point in time recovery down to a second, within the retention period 
- Automated Backups are enabled by default. The backup data is stored in S3 and you get free storage space equal to the size of your database. If you have an RDS instance of 10GB, you will get 10GB of storage
- Backups are taken within a defined window. During the backup window, storage I/O may be suspended while your data is being backed up and you may experience elevated latency
- Database Snapshots are done manually (ie they are user initiated.) They are stored even after you delete the original RDS instance, unlike automated backup
- Whenever you restore either an Automatic Backup or a manual Snapshot, the restored version of the database will be a new RDS instance with a new DNS endpoint

## Encryption at rest

- Supported by MySQL, Oracle, SQL Server, PostgreSQL, MariaDB and Aurora. It is done using the AWS Key Management Service (KMS). Once your RDS instance is encrypted, the data is stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas, and snapshots

## Multi-AZ 

- Allows you to have an exact copy of your production database in another AZ. AWS handles the replication for you, so when your production database is written to, this write will automatically be synced to the stand by database
- In the even tof a planned database maintenance, DB instance failure, or AZ failure, Amazon RDS will automatically failover to the standby so that the database operations can resume quickly without administrative intervention
- Multi-AZ support is available for the following DBs:
	SQL server
	Oracle
	MySQL Server
	PostgreSQL
	MariaDB

## Exam Tips

RDPS (OLTP)
 - SQL
 - MySQL
 - PostgreSQL
 - Oracle
 - Aurora
 - MariaDB

DynamoDB (No SQL)
Red Shift OLAP (Warehousing solution)
Elasticache to speed up performances of existing databases (frequent identical queries)