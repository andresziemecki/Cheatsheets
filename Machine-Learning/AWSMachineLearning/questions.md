# Data Engineering

## What Service can you use to store object files?
A blob (binary large object) storage S3. 

## How the system can access to the object quicky?
Using their full path, which is their key. 

## What's the max object size of an object in the blob store?
The max object size is 5TB.

## How you could set different security levels for different objects?
Assigning a tag to different buckets/objects. For example, we could set public which users can have access
or private which employees only have access.

## How you can speed up a query through you entire blob store?
Using partitioning, it means that we are going to have a well structure format in our buckets. Like:
`year/month/day/user_id` or `user_id/year/month/day` depending which is more convenient for your usecase

## Is it possible to save cost on s3 depending on how frequent are you going to access the data?
Yes, it is. Using storage classes:
- Standard
- Standard Infrequent Access (IA): less frequent but rapid access. Lower cost for storage but higher cost for retrival. 99.9% availability.
- One-Zone Infrequent Access: Better durability but less availability as the previous one. Applicacion: Data you can recreate. 
- Glacier instant Retrival: Great for once a quarter accessibility. Minimum storage duration is 90 days.
- Glacier Flexible Retrival: You get the data between 5 min to 12 hour depending your configuration.
- Glacier Deep archive: You will get the data in between 12 to 48 hours.
- Intelligent Tiering: Allows to move objects automatically between classes depending on their freq access. You can configure the timing if you want for moving objects.

## Can you move between classes after assignin them to one?
Yes, even you could use a lifecycle configuration to move objects automatically. For example, to assign a first class, then after some period of time another class, and so on. You can also set a time interval for automatic deletion. For example, you log files will be deleted after 365 days. You can set this rules for specific buckets or tags. You can use s3 Analytics to help you see with some reports when transition from one class to another.

## How you can handle easily a user storing the same object with a little modification each time?
You can use versioning in Amazon S3, is a means of keeping multiple variants of an object in the same bucket. You can use the S3 Versioning feature to preserve, retrieve, and restore every version of every object stored in your buckets. With versioning you can recover more easily from both unintended user actions and application failures. After versioning is enabled for a bucket, if Amazon S3 receives multiple write requests for the same object simultaneously, it stores all of those objects.

## How can you represent to a user how often are you going to lose one of its object?
With a Durability metric, like 99.9999999% of durability represent that you probably will lose one of its object in 10000 years.

## How do you represent to a user how often you will have available their objects in a period of time?
With the availability metric. Different storage classes have different availabilities. For s3 standard (%99.99 of availability) you will not have available an object an average time of 53min a year, instead you will get some errors.

## How can you add security to your s3 buckets?

Using Encryptation:
- SSE-S3: When you just want to encrypt files and the keys are handled and managed by aws. So, anyone with access to s3 can decrypt it
- SSE-KMS: You can set up a managment key service where now the user must have access to the key to decrypt. You can set this ecription by user based (IAM policies) or resource base (buckets).
- SSE-C: When you want to manage your own encryption key, basically you do the aws job management of SSE-KMS.
- Client Side encryption, you encrypt outside AWS before sending to s3.

You can also add a Networking security by setting a VPC Endpoint Gateway. Which allow traffic to stay between your VPC instead of going to the public web when for example transfering data between s3 and SageMaker.

## What service could be good for real-time big data? Which receives HUGE information like IoT, logs, metrics, clickstreams

AWS Kinesis it's a good tool for this, which is based on Apache Kafka. Which is a low latency streaming ingest at scale. Sharding and loadbalancing are the keys for succesfully handle the real-time big data. The data is available between 24hours or 365 days depending on the configuration. Multiple applications can consume these streams. The records can be up to 1Mb in size.

Each shard can be scale manually or automatically, it handle 1MB/s in (1000 records per second) for producers and 2MB/s out for consumers. You pay per shard provisioned per hour.

You can also have two more helpful services which go along with this one:

- Kinesis Analytics: real-time analytics in stream using SQL. You can perform SQL queries and send the result somewhere else. `Select * from stream_id where ...` We could also do continious metric generation for dashboards. Creating alers, etc. ML usecase: use random_cut_forest sql function for anomaly detection. Or hotspots function to detect places with more densities. 
- Kinesis Firehose: load steams into s3, redshift, elasticsearch, and Splunk. You can transform the record using lambda function and finally perform batch writes to any storage like s3, Redshift and ElasticSearch
- kinesis VideoStream: meant for streaming videos in real-time, where important consumers can be sagemaker or amazon recognition video.

## How can you build a service which can query data from s3 cheap and easily?

Building a service like Glue data catalogue. Which traverse with a crawler all buckets and store metadata about them like schemas and versions so you can later make queries very cheap and efficient. Then You can integrate it with Athena or Redshift. The catalog created depends on the buckets partitions. 

## What AWS Service is good for creating ETL jobs? Extract then Transform and then Load

Glue ETL is perfect for this. Just providing python code or Spark scripts. its build in serverless spark platform. You only pay per resource used per time. You can schedule the trigger or do it in base of an event.

It also has some builtin transformation for missing values, filters, join, map to a function, etc. Or ML transformation which delete similar rows.

## What service can be useful to query s3 data with glue data catalogue?

Athena, the result will be stored in an s3 bucket.

## How can you query data to s3 without glue?

You can use Redshift Spectrum.

## What can you use for tables organised by rows instead of columns like Redshift Do?

RDS Aurora is a SQL data store that organise the data by row instead of column. It's generally use for online transaction processing.

## What Database its noSQL and not in-memory based?

DynamoDB which is low latency, serverles and can also store machine learning models serverd by your application.

## Which database is good for logging?

OpenAearch, (previously elastic search) which it index the data and query them in a high efficiently way. 

## What orchestration services over your resources can be a good choice?

AWS Data Pipelines, which allow access to EC2 and EMR instances. The same creates resource in your own account in contrast to Glue ETL which is a serverless ETL.

## What's the difference between AWS MWAA and AWS Batch?

AWS MWAA uses Apache Airflow to create workflows and DAGS (Directed Acyclic Graphs) with Python to orchestrate complex, dependent tasks. AWS Batch is, as the name states, a batch processing service that utilizes docker containers. Batch allows you to manage instance types and container sizes to fine tune costs of workloads. Batch unlike MWAA does not utilize any orchestration service (you can use cloudwatch or stepfunctions for that), so apart from the queue that it utilizes, there is no way to control the workflow of tasks.

For AWS Batch you must provide docker image for any non-etl related work could also be useful.

If you have a job that requires complex workflows, AWS MWAA will reduce the complexity of managing those workflows. If you require large scale containerized processing for image analysis, data conversion, or ANY other job, AWS Batch will allow you to easily control your workloads to optimize speed and cost.

It should also be noted that AWS Step Functions is also a very efficient way to orchestrate various types of processing and application tasks. For simple tasks, there is very little overhead and management compared to AWS Batch or MWAA.

## How can you create a database migration services?

Using AWS DMS, which runs in an EC2 instance provided by you and do a continioues data replication.

Can migrate DB outside AWS and insert it into AWS.

## How can you orchestrate complex worflows?

Using AWS Step functions, which is built to design worflows, advance error handling and retrigger mechanism. You can execute this in paralel and have completely distinct worflow ways when some batch raise an error.

## Mention three ways to analyze data in s3:

1. Redshift Spectrum
2. EMR (Hadoop, hive, spark)
3. Athena

for 2 and 3 you can visualize it in Amazon QuickSight which is a visualization tool from AWS.

## What's the difference between AWS DataSync and AWS DMS?

AWS DataSync and AWS Database Migration Service (DMS) are both data migration services provided by AWS, but they serve different purposes.

AWS DataSync is a data transfer service that is designed to move large amounts of data between on-premises storage systems and AWS storage services. It is optimized for fast, efficient, and secure data transfers, and it supports a variety of storage systems and protocols.

AWS DMS, on the other hand, is a database migration service that is designed to migrate databases between different database management systems (DBMS) or data warehouses, including on-premises to AWS cloud migrations, AWS to AWS migrations, or vice versa. DMS supports a wide range of database sources and targets, including popular DBMS such as MySQL, PostgreSQL, Oracle, and SQL Server.

In summary, AWS DataSync is used for moving large amounts of data between storage systems, while AWS DMS is used for migrating databases between different DBMS or data warehouses.

## What is ECR?

Amazon Elastic Container Registry (Amazon ECR) is an AWS managed container image registry service that is secure, scalable, and reliable. Amazon ECR supports private repositories with resource-based permissions using AWS IAM. This is so that specified users or Amazon EC2 instances can access your container repositories and images. You can use your preferred CLI to push, pull, and manage Docker images, Open Container Initiative (OCI) images, and OCI compatible artifacts.

## What metrics for machine translation seq2seq are good?

BLEU Score and perplexity

