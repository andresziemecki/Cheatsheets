# Data Ingestion

The goal is to capture data, store them to then run ML algorithms.

We could have different streaming Ingestion in our application:

- ClickStream
- Change Data Capture
- Live Video

Which could happen through:

- Mobile App
- Voice Assistant
- Desktop

And potentially we could have millions per second.

## Clickstream

An ordered series of interactions that users have with some interface, like mouse clicks in a web browser. Interaction can also be touchscreen and conversational user interface.

This may have:

- Date/Time
- User-Agent (What type of browser, mobile app, desktop version of the web app, etc.)
- UserID (if logged in)
- Request Details (what pages they were looking at get/details/video_id)
- Session ID (Cookie, help ties clickstream entries)
- IP Address
- Referrer (How they found our website: google, facebook, etc)

TO handle millions of request, there are some good tools for it, like Kafka or Kinesis.



## Apache Kafka

An open-source software platform which provide a way to handle real-time data streaming.

Kafka acts ike a broker between our producers (Clickstream logs) and our consumers (Storage). If they amount of request coming is too high, then instead of having a single broker, we will have a broker cluster. Zookeper will act as the leader election for each partition and the configuration to handle different topics (home page, search page, etc.) for each broker.


### Zookeper

A service designed to reliably coordinate distributed systems via naming service, configuration management, data synchronization, leader election, message queing, or notification systems.

## Amazon Kinesis

An AWS product that provides a way to handle real-time data streaming.

Kinesis has shards instead of partitions which can scale up as our broker does in kafka. 

The producers can be anything, not only clickstreams, like any streaming ingestion aspect:

- Web crawler: Some script collecting data
- RSS Feed
- Storage such as another database

How we can ingest changes in our database? Is a process called Changes data capture

## Change Data Capture

The process of recording changes in the data within a database system. For instance, if a user cancel its Netflix suscription, then a row of a table will change to indicate that they're no longer subscribed.

The changes of this row can be recorded and referenced later for analysis or audit purpose.

This tool is used to keep track of the history of the users, like when he subscribed or unsuscribed, not just having in a table if he is subscribed.

So, in the change logs of each database system that we have:

- MySQL
- Cassandra
- MongoDB

We can send this changes to our broker, like Kafka, and our consumers will store this information.

OLTP -> Broker -> OLAP

## OLTP

Online transaction processing. A system that handles near real-time business processes. For example, a table that mantains a table of the users subscribed on Netflix and which is then used to enable succesful log-ins would be considered OLTP. This is opposed to OLAP

## OLAP

Online analytical processing. A system that handles the analytical processes of a business, including reporting, auditing and business intelligence. For example, this may be a Hadoop cluster which maintains users subscription history for Netflix. This is opposed to OLTP.

## Live Video

Ingesting video content from traffic cameras, security cameras, video streaming services.

Example: HLS - HTTP Live Stream, which effectively chops an mp4 into segments and send this segments over HTTP.

## Batch Ingestion

Is when we want periodic snapshots of the database.

Useful when onboarding a new database to be ingested. For example, the technologies that some databse uses to transfer to some particular database system

- MySQL: MySQL dump
- Cassandra: CQL copy
- MongoDB: mongoExport

## Ingestion COnsiderations

- Size of individual data. Like a clickstream or Live Video.
- Rate of the record comes to the broker.
- Support of data types. Such that our brokers can handle this data
- High availability (multi-AZ) and fault tolerance, so if a broker goes down, another can easily can take it place without any loses data. To avoid networking problems, we can add different availability zones.



## Availability Zone (AZ)

Typically a data center with two or more regions with more data centers. The term "multi-AZ" implies that an application or software resource is presented across more than one AZ within a region. This strategy allows the software resource to continue operating even if a data center becaomes unavaliable.


## Example 
There is an example of starting a zoopeker with kafta in the vidoe. Also integrated with a producer and a consumer.