
# Load Balancers

A type of reverse proxy that distributes traffic acrosss servers. Load balancers can be found in many parts of a system, from the DNS layer all the way to the database layer.

## Server Selection Strategy

How a load balancer choose servers when distributing traffic amongst multiple servers. Commonly-used strategies include:

- **round robbin**: Happens at the DNS layer where a single domain name gets multiple IP addresses and when the DNS name gets the request, returns an IP address in a load balance way. For example, if you execute `dig google.com` in your terminal which give you the IP address of a certain domain, you will see different IP addresses when executing multiple times.
The round robbins just go one by one and distributing uniformly during all instance. Then you have a weight round robbin where you can use it when you will have sometimes mroe powerful machines than others.
- **Random Selection**
- **performance-based selection**: choosing the server with the best performance metrics, like the fastest response time or the least amount of traffic. 
- **IP-based routing**: Is going to hash the IP address of the client and it redirect that traffic. 
- **Path-based**: Redistributes the requests According to the path of the request

Some of them are software load balancers, and others hardware load balancers. 

You could have multple load balancers on different parts of the system or in the same system.

What happend if a load balancers is overloaded? You can put more where they can comunicate between each other.

## Hot Spot

When distributing a workload across a set of server, that workload might be spread unevenly. This can happen if your **sharding key** or your **hashing function** are suboptimal, or if your workload is naturally skewed: Some servers will receive a lot more traffic than others, thus creating a "hot spot".

## Nginx

See it in the previous section but remember that this could be used as a load balancer.

There is a way to configure it as load balancers and add weights in the conf file.