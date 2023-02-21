
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