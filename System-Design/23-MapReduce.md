# Map Reduce

Map reduce is a programming model for processing and generating big datasets in parallel, distributed algorithm on a cluster.

It is a popular framework for processing very large datasets in a distribute settings efficiently, quickly, and in a fault tolerant manner.

A map reduce job is comprised of 3 main steps:

1. **Map** step, which runs a map function on the various chunks of datasets and transform each chunk into intermediate a key-value pairs.

2. **Shuffle** step, which reorganise the intermediate key-value pairs such  that pairs of the same keysare routed to the same machine in the final step.

3. **Reduce** step, it uses a reduce function into this newly key-value paris to transforms them into more meaningful data.

The canonical example of MapReduce case is to count the number of occurences of words in a large text file.

When dealing with MapReduce library, engineers and/or system administrators only need to worry about the map and reduce function. as well as their inputs and outputs. All the other concerns, including the paralelization task and the tolerance of the MapReduce job, are abstracted away and taked care by the MapReduce implementation.

A MapReduce that I can imagine is that given a large file, you splitted in chunks and then count the number of occurrencies of each words appear. Like a Counter in python. That's the map function that produce the key-value pairs. Then the reduce function will be the combination of these Counter maps summing their values for each pair of key.

You could apply the same example with latencies except a text of words. So they map will be if a latency is bigger than 10 sec, put one in one file, otherwise put a 1 in another file so we get the intermediate steps which is files of values that belongs to the key(latency)-value(a 1 in file i) pair for each host that process one latency file. Then it goes the shuffle step which the machine grab the key of the file name of a specific host and read the content and write to the final map result file the result which are files of a combination of the host files. Finally we add the reduce step, which get the reduces as input (those 1 values) and count how many times we have a 1 on each file.

## Distributed File System

It is an abstraction over a cluster (usually large) of machines that allows them to act like one large file system. The two most popular DFS are the Google File System (GFS) and the Hadoop Distributed File System (HDFS).

Typically, DFSs take care of the availability and replication guarantees that can be tricky to obtain in a distributed system settings. The overarching idea is that files are splitted into chunks of smaller sizes (4-64Mb, for instance) and those chunks are shared into a large cluster of machines. A central control pannel is in charge to decide where each chunks resides, routing reads to the right nodes, and handling communication between machines.

Different DFS implementation has slightly different APIs and semantics, but they achieve the same common goal: extremely large-scale persistent storage.

## Hadoop

A popular, open-source framework that supports MapReduce jobs and any other kind of data-processing pipelines. Its central component is HDFS (Hadoop Distribute File System), on top of which other technologies have been developed.

[link here](https://hadoop.apache.org)