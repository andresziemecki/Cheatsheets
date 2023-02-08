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
