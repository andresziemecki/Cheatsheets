
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
