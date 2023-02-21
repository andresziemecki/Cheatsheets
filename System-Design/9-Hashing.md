

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