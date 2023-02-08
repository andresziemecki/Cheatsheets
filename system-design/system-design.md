

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

# Replication and Sharding

If the databse is down, your system might be down, so that's why replication exists. The main database has all the reads and writes, but it also updates the replica. The operation sometimes might take longer because the data must be inserted in the main and the replica.

Sometimes we don't have to update inmediatly like the feed of instagram. People from different countries has different database and they sync each other eventually after some interval of time.

## Replication

The act of duplicating the data from one server to others. This is sometime to increase the redundancy of your system and tolerate regional failures for instance. Other times you can use replication to move data closer to your clients, thus decreasing the latency of accesing specific data.

## Sharding

Sometimes called data partitioning, sharding is the act of splitting the database into two or more pieces called **shards** and is typically to increaste the throughput of your database. And you avoid duplicating so much data by normal replication to increaste the throughput. Popular sharding strategies include:

- Sharding based on a client's region
- Sharding based on the data being stored (User data gets stored in one shard, payments data get stored in another shard)
- SHarding based on a hash of a column (only for structured data)

Soemtimes you would like to have replicas of each shard to increase the availability and redundancy.

## Hot Spot

When distributing a workload on a set of servers, that workload might be spread unevenly (some shards receive more traffic that others). This can happen if your sharding key or your hashing function are suboptimal, or if your workload is naturally skewed: some servers will receive more traffic than others, that creates a *Hot Spot*.