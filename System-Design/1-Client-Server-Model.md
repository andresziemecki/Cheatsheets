# Client-Server Model

## Client

A machine or process that request data or service from a server.
Note that a single machine or piece of software can be both a client and a server at the same time. For instance, a single machine could act as a server for end users and as client for database.

## Server

A machine or process that provides data or service to a client, usually by listening for incoming network calls. Note that a single machine or piece of software can be both, a client and a server at the same time. For instance, a single machine could act as a server for end users and as a client for database.

## Client-Server Model

The paradigm by which the modern systems are designed, which consist on client requesting data or service from servers and servers providing data or service to client.

Simplified Model:
```
Client -> Server
Server -> Client
```
What Really happens
```
Client -> DNS Query -> IP Adress
IP Adress -> Client
```

## DNS

Short for *Domain Name System*, it describes the entities and protocols involve in the translation from domain names to IP addresses. Typically, machine makes a DNS query to a well-known entity which is responsible for returning the IP address (or multiple ones) of the requested domain name in the response. In other words it's a special request that goes to predeterminate servers and ask where is the webpage. 

## IP

Unique identifier for Machine. It's an address given to each machine connected to the public internet. IPV4 address consist of four numbers separated by dots: *a.b.c.d* where all numbers are between 0 and 255. Special values include:
- 127.0.0.1: Your own local machine. Also referred as **localhost**.
- 192.168.x.y: Your private network. For instance, your machine and all machines from your private wifi netowork will usually have the 192.168 prefix.

If you hit `dig algoexpert.io` in your terminal it's going to request a dns query and we'll get as a response the IP adress of that website. Then we can end the http request directly to the website.

## HTTP

It is a protocol. A protocol is a way to send information that your browser will understand.

Inside your request is the same address of your computer and that is going to be the source address for your request.

## Ports

In order for multiple programs to listen for multiple network connections on the same machine without colliding. they pick a port to listen on. A port can be represented as an integer between 0 and 2^16 (~6500). The machine has 2^16 total ports.

In other words, servers listen on request on specific ports. Any machine that has a distinct IP address has 16 000 ports. So, when you do a request, you've to specify the port that you're listening. The client knows the port depending on the protocol. For example, 
- If it tries to use HTTP protocol -> port uses is 80
- If it tries to use HTTPS protocol -> port uses is 443

Typically, ports 0-1023 are reserved for system ports. (also-called well *known-ports*) and should't be use by user-level processes. Certain ports has predefine uses, and although you usually won't be required to have them memorized, they sometimes can come in handy. Below are some examples:

- 23: Secure Shell.
- 53: DNS lookup.
- 80: HTTP.
- 433: HTTPS.

## NC

net cat command: write/read to network connection. For example, open two terminales, in one of them hit 
```
nc -l 8081
```
which means listen to this port, and the other one hit 

```
nc 127.0.0:1 8081
``` 
which means communicate from 1 (from your machine) to port 8081. The one (1) means always point to your local machine. Now start typing in the second terminal and you will see how the first terminal listen to all the things that you are writing.