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