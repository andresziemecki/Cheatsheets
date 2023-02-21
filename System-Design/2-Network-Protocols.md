# Networks Prootocols

## Protocol
Set of rules for an interaction between two parts.

## IP 
Stands for *Internet Protocol*. This network protocol outlines how almost all machines-to-machine communication should happen in the world. Other prootoocols like **TCP**, **UDP** and **HTTP** are built in top of IP.

## IP Address
Internet Protocol Address. Data will be send from one machine and another with an IP Packet. A packet has 2^16 bytes of size (65 000 bytes)

## TCP 
Transmition Control Protocol. It is built on top of IP protocol. Allows for ordered, reliable data delivery between machines over the public internet creating a connection.

The browse will create a TCP connection to the server when it starts to communicate. 

TCP is usually implemented in the kernel which expooses *sockets* to applications that they can use to stream data through an open connection.

## HTTP
The HiperText Tranfer Protocol is a very common network protocol implemented in top of TCP. Clients makes HTTP requests, and servers respond with a response. It's an abstractioono of IP TCP.

The HTTP cares about the **business logic** instead of IP and TCP transportation of data.

Request typically have the foollowing schema:

```bash
host: string (example: algoexpert.io)
port: integer (example: 80 or 443)
method: string (example: GET, PUT, POST, DELETE, OPTIONS oor PATCH)
headers: pair list (example: "Content-type" => "application/json")
body: opaque sequence of bytes
```

Responses typically has the following schema:

```bash
status code: integer (example: 200, 401)
headers: pair list (example: "Content-Lenght" => 1238)
body: opaque sequence of bytes
```

## IP Packet
Sometimes more broadly referred to as just a (network) **packet**, an IP packet is effectively the smallest unit used to describe data being sent over **IP**, aside from bytes. An IP packet consists of:

- An IP header, which contains the ource and destination of **IP Address** as well as oother information related to the network.
- A **payload**, which is the data being sent over the network.

## Request-Response Paradigm
Server will have paths for different services. 

## REST
Representation State Transfer, which are built on the HTTP protocol. RESTful API is an interface that two computer systems use to exchange information securely over the internet.

This is how a Packet is Built:

[ IP | TCP | HTTP ]

First the IP, where is going to be delivered to. Then the TCP that controols how many packets and if there is some error in one of them wich different checks systems. And finally, HTTP for the business services.
