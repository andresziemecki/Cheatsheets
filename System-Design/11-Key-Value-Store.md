


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

## Redis

An in-memory key-value store. Does offer some persistent storage options but is typically used as really fast, best-effort caching solution. Redis is also often used to implement rate limiting.

https://redis.io

Redis (Remote Dictionary Server) is a fast, reliable, and open-source datastore famous for caching, session management, and real-time analytics. It supports a wide array of data structures, including Hashes, Strings, Bitmaps, Lists, Sets, and Sorted Sets. Furthermore, Redis uses the BSD license, which means you can freely use it for commercial purposes.

## ZooKeeper

Zookeeper is a strongly consistent, highly available key-value store. It's often used to store important configuration or to perform leader election.

https://zookeeper.apache.org
