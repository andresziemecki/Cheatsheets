# Availability

The odds of a particular server or service being up and running at any point in time, usually measured in percentages. A server that has 99% of availability will be operational 99% of the time (This would be described as having two nines of availability). I think the opposite it's `downtime`.

In other words, it's the description of a services for fault tolerances. 

It's important for customer doe't have bad experience.

## High Avilability

Used to describe systems that have particualrly high levels of availability, typically 5 nines or more; sometimes abbreviated as `HA`.

## Nines

Typically refers as percentages of uptime. For example, 5 nines of availability means an uptime of 99.999% of the time. Below are the downtime expected per year depending on those 9s:

```
- 99% (two nines): 87.7 hours
- 99.9% (three nines): 8.8 hours
- 99.99%: 52.7 minutes
- 99.999%: 5.3 minutes
```

## How to improve Availability

You want make sure your system doesn-t have single point of failers. Which if this point fails, your ENTIRE system will fail. And we can reduce the system point of failures by adding redandancy.

## Redundancy

The process of replicate parts of a system in an effort to make it more reliable. By adding more servers to make your system more redundant, you will need to add a load balancer, which can fails also... So you have to add more load balancers to add redundancy

## Passive redundancy

If one server or load balancer fails, doesn-t matter because we have others running. Like the turbins of the airplane, if one fail, the airplane can fly smoothly without problems using just one turbine.

## Active redundancy

Only one or few of the machine are typically handling the traffic and doing the work. If this one fails the other machines need to know about this and have to take action to take its place. This is where `leader election` comes to play, that we are going to see it later.

## SLA

Short of `service-level-agreement`, an SLA is a collection of guarantees given a customer by a service provider. SLAs typically make guarantees on a system's availability, among other things. SLAs are made up of one or multiple SLOs.

In other words, they garantee you X level of uptime in the system.

## Reminders

You want rigourous process in place to handle system failures, and handle things manually with alrtes and msgs if everything crash or something really bad happens.


## SLO

Short of `services-level objective`, an SLO is a guarantee given to the customer by a services provider. SLOs typically make guarantees on a system's availability, amongst other things. SLOs constitute an SLA.

It's a component of SLA. So an SLA as multple SLOs. The percentage of garaantee of the uptime will be the SLO. If the services tells you that you will have X numbers of errors, that would be another SLO.

## GCP or AWSs

these providers has the SLAs in their websites. And also they provide what they will do if they fail this SLA. 
