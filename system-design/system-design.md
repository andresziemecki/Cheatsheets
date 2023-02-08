# Storage

## Databases

Databases are programs that either use disk or memory to do 2 core things: record data and query data. In general, they are themselves servers that are long lived and interact with the rest of your application through network calls, with protocols on top of TCP or even HTTP.

Some database only keep records in memory, and the users of such databases are aware of the fact that those records may be lost forever if the machine or process dies.

For the most part though, databases needs persistance of those records, and thus cannot use memory. This means that you have to write your data to disk. Anything written to disk will remain through power loss or network partitions, so that's what it used to keep permanent records.

Since machine die often in a large scale system, special disk partitions or volumenes are used by the database processes, and these volumnes can get recovered even if the machine were to go down permanently.

## Disk

Usually refers to either HDD (hard-disk drive) or SSD (solid-state drive). Data written to disk will persist through power failures and general machine crashes. Disk is also referred to as non-volatile storage.

SSD is far faster than HDD, but also far more expensive from a financial point of view. Because of that, HDD will typically be used for data that's rarerly accessed or updated, but that's stored for a long time, an SSD will be used for data that is frequently accessed and updated.

## Memory

Short for Random Access Memory (RAM). Data stored in memory will be lost when the process that has written that data dies.

## Persistent Storage

Usually refers to disk, but it refers to any form of storage that persist if the process in charge of managing it dies.

## Distribute storage

Store data in multiple machine to atack different problems, like consistency por example. When we try to solve those problems, then a question may arise with your implementation: Are you going to get staleless data or the last updated one?

# Latency and Throughput

Two important measures of a system. Accuracy (How accurate is the data provided) and uptime (how much time is up and running vs total time) are another two measures in a system.

These measurement are not correlated, if there is high latency doesn-t mean it will have high throughput.

## Latency

The times it takes to a certain operation to complete in a system (for example, for the client to the server and then from the server to the client). We can also split the total latency in sublatency and measure each part. Most often this measure is a time duration, like milliseconds or seconds. You should know these orders of magnitude:

- Reading 1MB from RAM: 0.25ms
- Reading 1MB from SSD: 1ms
- Transfer 1MB over network of 1Gbps (One Giga Bit per second) is 10ms.
- Reading 1MB from HDD: 20ms
- Inter Continental Round trip: 150ms

## Throughput

The number of operations that a system can handle properly per time unit. For instance the throughput of a server can often be measured in request per seconds (RPS or QPS). Typically we measure throughput in Gbps or Mbps. In other words, how many request per second and at the same time the request can be converted into bit and then you get how many bit per seconds you have for throughput.

# Availability

The odds of a particular server or service being up and running at any point in time, usually measured in percentages. A server that has 99% of availability will be operational 99% of the time (This would be described as having two nines of availability). I think the opposite it's `downtime`.

In other words, it's the description of a services for fault tolerances. 

It's important for customer doe't have bad experience.

## High Avilability

Used to describe systems that have particualrly high levels of availability, typically 5 nines or more; sometimes abbreviated as `HA`.

## Nines

Typically refers as percentages of uptime. For example, 5 nines of availability means an uptime of 99.999% of the time. Below are the downtime expected per year depending on those 9s:

```
- 99% (two nines): 87.7 hours
- 99.9% (three nines): 8.8 hours
- 99.99%: 52.7 minutes
- 99.999%: 5.3 minutes
```

## How to improve Availability

You want make sure your system doesn-t have single point of failers. Which if this point fails, your ENTIRE system will fail. And we can reduce the system point of failures by adding redandancy.

## Redundancy

The process of replicate parts of a system in an effort to make it more reliable. By adding more servers to make your system more redundant, you will need to add a load balancer, which can fails also... So you have to add more load balancers to add redundancy

## Passive redundancy

If one server or load balancer fails, doesn-t matter because we have others running. Like the turbins of the airplane, if one fail, the airplane can fly smoothly without problems using just one turbine.

## Active redundancy

Only one or few of the machine are typically handling the traffic and doing the work. If this one fails the other machines need to know about this and have to take action to take its place. This is where `leader election` comes to play, that we are going to see it later.

## SLA

Short of `service-level-agreement`, an SLA is a collection of guarantees given a customer by a service provider. SLAs typically make guarantees on a system's availability, among other things. SLAs are made up of one or multiple SLOs.

In other words, they garantee you X level of uptime in the system.

## Reminders

You want rigourous process in place to handle system failures, and handle things manually with alrtes and msgs if everything crash or something really bad happens.




## SLO

Short of `services-level objective`, an SLO is a guarantee given to the customer by a services provider. SLOs typically make guarantees on a system's availability, amongst other things. SLOs constitute an SLA.

It's a component of SLA. So an SLA as multple SLOs. The percentage of garaantee of the uptime will be the SLO. If the services tells you that you will have X numbers of errors, that would be another SLO.

## GCP or AWSs

these providers has the SLAs in their websites. And also they provide what they will do if they fail this SLA. 

# Caching

Commonly used to reduce or improve the latency of a system. Or reduce the number of request you do to something very popular.

**Redis** is a very popular in memory database.

You can write in cache and database and they will be in sync.

## Cache

A peace of hardware or software that stores data, typically meant to retrieve that data faster than otherwise.

Cache are often use to store to store responses to network requests as well as results of computationally-long operations.

Note that data in a cache can become `stale` if the main source of truth for that data (i.e, the main data behind the cache) gets updated and the cache doesn't.

## Type of Caches

* Write through cash: Is a type of caching system that when you write a peace of data, your system will write that peace of data both in the cache and in the main source of truth at the same time. So the cache and the database are always in sync. THe donwside of this, is that you still need to go to the database. 

* Write back cache: The server update only the cache and not the database. So now the cache will be out of sync with the database.
THe system will asynchronally update the database with the cache. You slow down the the rpm to the database but if you loose the data in cache for some reason, you will not have the database updated and you will lose the data. 

## Cache Hit

When requested data is found in the cache.

## Cache Miss

When requested data could be found in a cache but isn't. This is typically used to refer to negative consequence of a system failure or of a poor design choice. For example:

If a server goes down, our load balancer will have to forward requests to a new server, which will result in a cache miss.

## Cache Eviction Policy

The policy by which valus get evicted or removed from a cache. Popular cache eviction policies include **LRU** (least-recently used), **FIFO** (first-in first-out), and **LFU** (least-frequently used).

## Content Delivery Network

A **CDN** is a third party service that acts like a cache for your servers. Sometimes, web applications can be slow for users in a particular region if your servers are located only in another region. A CDN has servers all around the world, meaning that the latency to a CDN's servers will almost always be far better than the latency to your servers. A CDN's servers are often referred to as **PoPs** (Points of presence). Two of the most popular CDN are **Cloudfire** and **Google Cloud CDN**.

## YouTube Comment section

If every video update in caches the comments of the videos, caches can become stale if they haven't been updated properly in all machines, old comments will start to mix with new comments when replying comments. But we can use a unique cache like Redis to interact with all our servers instead using the cache of each machine.

## When use Redis or normal caching?
This depend on how much we care about the accuracy of the data in the system. 

## Pitfails

If the data we are dealing with is static data and unmutable the cache is beautiful. If the data is mutable everything starts to be tricky because you will have different data in different servers.

If you don-t care about consistency, staleness, you will totally consider caching because you don-t have to worry about the potential pitfails. 

## How do we actually get rid of data?

Depend of the use case.

1. LRU policy (get rid of the least recently used peace of data in a cache)
2. LFU policy (get rid the least frequently used)
3. FIFO bases
4. Randomly

# Proxies

## Forward Proxy

A server that sits between a client and servers and acts on behalf of a client, typically used to mask the client's identity (IP address). Note that forward proxies are refered to as just proxies.

Typically configured by the client. The forward proxy get the request from the client and then to the server. Then the server respond to the fowrad proxy and finally to the client.

Sometimes it is used to hide the request from the client. So, the source IP address is going to the forward proxy instead of the client. And this is how basically how VPN works, where you can access website where your country is unavailable.


## Reverse Proxy

A server that sits between clients and servers and acts on behalf of the servers, typically used for logging, load balancing, or caching.

This acts on behalf of a **server**. It is configured by the server. The client think that the request go to the destination but in reality it goes to the reversed proxy. The client send the request to the proxy, proxy to the server and then the other way around.

To the client there are no two entities, he doesn't see.

You can also filter request some request with your reversed proxy. Or take care of login. Cache stuffs. The best use case is the load balancer.

## Nginx

Pronounced "engine-X" not N-jinx, Nginx is a very popular webserver that's often used as a reversed proxy and load balancer.

It's a web server that can be used as a reverse proxy. 

https://nginx.com

# Load Balancers

A type of reverse proxy that distributes traffic acrosss servers. Load balancers can be found in many parts of a system, from the DNS layer all the way to the database layer.

## Server Selection Strategy

How a load balancer choose servers when distributing traffic amongst multiple servers. Commonly-used strategies include:
- round robbin: Happens at the DNS layer where a single domain name gets multiple IP addresses and when the DNS name gets the request, returns an IP address in a load balance way. For example, if you execute `dig google.com` in your terminal which give you the IP address of a certain domain, you will see different IP addresses when executing multiple times.
The round robbins just go one by one and distributing uniformly during all instance. Then you have a weight round robbin where you can use it when you will have sometimes mroe powerful machines than others.
- random selection
- performance-based selection: choosing the server with the best performance metrics, like the fastest response time or the least amount of traffic. 
- IP-based routing: Is going to hash the IP address of the client and it redirect that traffic. 
- Path-based: Redistributes the requests According to the path of the request

Some of them are software load balancers, and others hardware load balancers. 

You could have multple load balancers on different parts of the system or in the same system.

What happend if a load balancers is overloaded? You can put more where they can comunicate between each other.

## Hot Spot

When distributing a workload across a set of server, that workload might be spread unevenly. This can happen if your **sharding key** or your **hashing function** are suboptimal, or if your workload is naturally skewed: Some servers will receive a lot more traffic than others, thus creating a "hot spot".

## Nginx

See it in the previous section but remember that this could be used as a load balancer.

There is a way to configure it as load balancers and add weights in the conf file.

# Hashing

## Hashing Function

A function that takes in a specific data type (such as string or an identifier) and outputs a number. Different inputs may have the same output, but a good hashing function attempts to minimize those hashing collisions (which is equivalent to maximizing uniformity).

There are two very popular hashing used in load balancers: Consistent Hashing and Rendezvous Hashing. It's useful in some cases becase for example, if we have a random selection and a client C1 request something two times, the request will end in different servers (let's say A and B) and we will have cached the same thing twice in both. This doesn't happen when we use hashing.

The problem with normal hashing is when we have to add new servers. The hashing function will compute total different numbers (coz of the mod function %) from all the client that have been requesting data before. So, all our caches are no more useful because the request of each client now are redirected to a different server. That's when the Consistent and Rendezvous Hashing comes to play.

## Consistent Hashing

A type of hashing that minimizes the number of keys that needs to be remapped when the hash table gets resized. It's often used by load balancers to distribute traffic to servers. It minimizes the number of requests that get forwarded to different servers when new servers are added or when existing servers are brought down.

The basic idea how it works, is to put the servers in a place of a discrete numbers inside a circle. So, when a new server comes, it is put in one position of the circle. Then when a new request arrive, the number after the hash function will arrive to one point into te circle and if it doesn-t find anything, it moves clockwise till get a server address. So adding a new server is not more a problem, the same apply when a servers die. In other words it doesn't change too much the redirection after each server is added or deleted.

You can weight it also, you can imagine the same thing as before but instead of adding the server into the circle just once, you can add it in different places multple times depending on how much powerful the server you are adding is. So, there is a higher likelihood to end in the most powerful server.

## Rendezvous Hashing

A type of hashing also coined **highest random weight** hashing. Allows for minimal re-distribution of mapping when a server goes down.

Rendezvous or highest random weight hashing is an algorithm that allows clients to achieve distributed agreement on a set of k options out of a possible set of n options. A typical application is when clients need to agree on which sites objects are assigned to.

What does in a nutshell is that computes a score between the client and the user and the max score is the server that we return.
So, the score will reminds the same between a server and a client if we add a new server. At the end very few clients will be redirected to another server.

## Advantage and disadvantage of Consistent and Rendezvous Hashing

Both consistent hashing and rendezvous hashing are algorithms that can be used in distributed caches to decide the home server for any given key, and can often be replaced with each other in most practical use cases. But there are some differences between them, which can make one of these a little more suitable for some conditions.

- Rendezvous hashing is much simpler to understand and code.
- Rendezvous hashing provides a very even distribution of keys on each node, even while node are being added/removed. Consistent hashing can fail to provide an even distribution for small clusters (though this can be fixed to a large extent by using many virtual replicas for each node). This is the biggest advantage of Rendezvous hashing over consistent hashing.
- Consistent hashing is typically done in  O(logN)  time using a binary search. Rendezvous hashing is typically done in  O(N) time, though it can also be done in O(log N). Also,  N  in consistent hashing is larger, often by a factor of ~100, since consistent hashing needs to create virtual nodes as well.
- Consistent hashing requires just one hash computation per key, whereas Rendezvous hashing requires  O(N)  hash computations per key. This can make a difference if you're using a slow hash function and have a large ring size.
- Consistent hashing requires some fixed memory to work well (mapping nodes to virtual nodes and hashes for all the virtual nodes) whereas Rendezvous hashing doesn't require storing any additional data.
- Rendezvous hashing can naturally provide  k  different servers for any key. This makes it very useful to support replication. While consistent hashing can also be modified to do this, it's not a 'standard part' of consistent hashing algorithm/implementation.

So in nutshell, use Rendezvous hashing if:

- Your clusters are very small.
- Your clusters are very large (say thousands of nodes) and you need to keep your memory footprint low.
- You want to support replication, but don't want to implement a slightly modified consistent hashing algorithm yourself.

## SHA

Short for *Secure Hash Algorithm*, the SHA is a collection of cryptographic hash functions used in the industry. These days, SHA-3 is a popular choice to use in a system.

# Relational Databases 

A type of structure database in which data is stored following a tabular format (tabular-like structure); often supports powerful querying using SQL. In toher words, it's going to be store in the form of tables. Tables are also called relations in a relational database. These tables follows a special schema, with a specific data type on each column.

## Non-Relational Database

In contrast with relational database (SQL database), a type of database that is free of imposed, tabular-like structure (They don't imposed this tabular data format). Non-relational database are often referred as to as NoSQL databases.

## SQL

Structure Query Language. Relational databases can be used using a derivate of SQL such as PostgreSQL in the case of Postgress.
Is effectly a programming language for database. It is used to perform complex queries in relational databases and perform data operations in a very efficient way.

Most relational database supports SQL, but not all of them. 

## SQL Database

Any database that supports SQL. This term is often used synonymosly with "Relational Database", though in practice, not every relational database supports SQL.

## NoSQL Database

Any database that is not SQL compatible is called NoSQL.

## ACID Transaction

A type of database transaction that has four important properties:

1. **Atomicity**: The operations that construct the transaction will either **all** succeed or **all** fail. There is no in-between state. If for some reason one fails because of lost networking, all will fail.
2. **Consistency**: The transaction cannot bring the database to an invalid state. After the transaction is commited or rolled back, the rules for each record will still apply, and all future transactions will see the effect of the past transactions. ALso named Strong Consistency.
3. **Isolation**: The execution of multiple transaction concurrently (at the same time) will have the same effect as if they have been executed sequentially. Remember Clements example, when you begin a transaction twice (from two terminals), one will be in a wating mode till the other when will commit.
4. **Durability**: Any commited transaction is written to non-volatile storage. It will not be undone by a crash, powr loss, or network partition.

## Databse Index

A special auxiliarity data structure that allows your database to perform certain queries much faster. Indexes can typically only exist to reference structured data, like data stored in relational database. In practice you create an index on one or multple columns in your database to greatly speed up read queries that you run very often, with the downside of slightly longer writes to your database, since writes have to also take place in the relevant index because the datatype is more complex.

## Strong Consistency

Strong Consistency usually refers to the consistency of ACID transactions, as opposed to Eventual Consistency.

## Eventual Consistency

A consistency model which is unlikly Strong Consistency. In this model, reads might return a view of the system that is stale (old). An ventually consistency datastore will give guarantees that the sate of the database will eventually reflect writes within a time period (could be 10 seconds, or minute).

## Postgress

A relational database that use a dialect of SQL called [PostgreSQL](https://postgresql.org). Provides ACID transactions.

# Key-Value Stores

A key-value store is a flexible NoSQL database that's often used for caching and dynamic configuration. Popular options include DyanmoDB, Etcd, Redis, and Zookeeper.

They are flexible because they do not impose structure and simple because maps a key to a value.

Using key value stores lowers latecy and increase throughput in every part of your system. 

There are some of them that writes (persist) the data on disk so they are not going to lose the data even if the machine goes down or crashes. Other writes data in memory like Redis. So if they crash you lose the data, but it's extremely faster.

Ones give you strong consistency (returns stale/old data or not) and other not.

## Etcd

It's a strongly consistent and highly available key-value store that's often used to implement leader election in a system.

https://etcd.io

## DynamoDB

Amazon DynamDB is a reliable, scalable, and robust NoSQL database fully managed by AWS. It is capable of delivering single-digit millisecond performance on any scale. As a result, this database service is highly efficient for any web, mobile, or gaming applications that require low latency data access.

On the other hand, Redis (Remote Dictionary Server) is a fast, reliable, and open-source datastore famous for caching, session management, and real-time analytics. It supports a wide array of data structures, including Hashes, Strings, Bitmaps, Lists, Sets, and Sorted Sets. Furthermore, Redis uses the BSD license, which means you can freely use it for commercial purposes.

## Redis

An in-memory key-value store. Does offer some persistent storage options but is typically used as really fast, best-effort caching solution. Redis is also often used to implement rate limiting.

https://redis.io

## ZooKeeper

Zookeeper is a strongly consistent, highly available key-value store. Ot's often used to store important configuration or to perform leader election.

https://zookeeper.apache.org

# Specialized Storage Paradigm

## Blob Storage 

*Blob* stands for binary large object. But people refer to some arbitrary peace of unstructured data. It's not easy to implement on by yourself. You will always rely on using one existing blobstore.

Widely used kind of storage, in small and large scale systems. They don't count as a database per se, partially because they only allow the user to store and retrieve data based on the name of the blob. This is sort of like key-value store but usually blob stores have different guarantees. They might be slower than KV stores but values can be megabytes large (or sometimes gigabytes large). Usually people use this to store things like large binaries, database snapshots, or images and other static assets that a website might have.

Key-value store are more optimize for latency rather than availability and durability.

## Times Series Database

A TSDB is special kind of database optimized for storing and analyzing time-indexed data: data points that specifically occur at a given moment in time. Examples of TSDBs are InfluxDB, Prometheus, and Graphite.

They are often used for monitoring and logging purposes. They are also used to store cryptocurrency prices, where it is stored the price every second or millisecond. 

So in a interview, we can rely on a monitoring system using InfluxDB por example.

## Graph Database

A type of database that stores data following the graph data model. Data entries in a graph database can have explicitly defined relationshipts, much like nodes in a graph can have edges.

Graph databases take advantage of their underlying graph structure to perform complex queries on deeply connected data very fast.

Graph database are thus often preferred to relational databases when dealing with systems where data points naturally form a graph and have multple levels of relationshipts - for example, social networks.

## Cypher

A graph query language that was originally developed for the Neo4j graph database, but that has since been standaried to be used with other graph databases in an effor to make it the "SQL for graphs".

Cypher queries are often much simpler than their SQL counterparts. Example Cypher query to find data in Neo4j, a popular graph database:

```
MATCH (some_node:SomeLabel)-[:SOME_RELATIONSHIP]->(some_other_node:SomeLabel
{some_property:'value'})
```

## Spatial Database

A type of database optimized for storing and querying spatial data like locations on a map. Spatial databases rely on spatial indexes like **quadtrees** to quickly perform spatial queries like finding all locations in the vicinity of a region.

## Quadtree

A tree data structure most commonly used to index two-dimensional spatial data. Each node in a quadtree has either zero children nodes (and is therefore a leaf node) or exactly four children nodes.

Typically, quadtree nodes contain some form of spatial data-- for example, locations on a map -- with a maximum capacity of some specified number **n**. So long as nodes aren-t at capacity, they remain leaf nodes; once they reach capacity, they're given four children nodes, and their data entries are split across the four children nodes.

A quadtree lends itself well to storing spatial data because it can be represented as a grid filled with rectangles hat are recursively subdivided into four sub-rectangles, where each quadtree node is represented by a rectangle and each rectangle represents a spatial region. Assuming we're storing locations in the world, we can imagine a quadtree with a maximum node-capacity **n** as follows:

- The root node, which represents the entire world, is the outermost rectangle.
- If the entire world has more than **n** locations, the outermost rectangle is divided into four quadrants, each representing a region of the world.
- So long as a region has more than **n** locations, its corresponding rectangle is subdivided into four quadrants (the corresponding node in the quadtree is given four children nodes).
- Regions that have fewer than **n** locations are undivided rectangles (leaf nodes).
- The parts of the grid that have many subdivided rectangles represent sparsely populated areas (like rural areas).

Finding a given location in a perfect quadtree is an extremely fast operation that runs in log4(x) time (where x is the total number of locations), since quadtree nodes have four children nodes.

## Google Cloud Storage

GCS is a blob storage service provided by Google.

## S3

S3 is a blob storage services provided by Amazon through Amazon Web Services (AWS).

## InfluxDB

A popular open-source time series database.

https://influxdata.com

## Prometheus

A popular open-source time series database, typically used for monitoring purpose.

https://prometheus.io

## Neo4j

A popular graph database that consists of nodes, relationships, properties, and labels.

https://neo4j.com

