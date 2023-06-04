# Leader Election

Citizens in a society typically elect a leader by voting for their preferred candidate. But how do servers in a distributed system choose a master node? Via algorithms of course!

## Leader Election

The process by which nodes in a cluster (for instance, servers in a set of servers) elect a so-called "leader" amongst them. He is responsible for the primary operations of the service that these nodes support. When correctly implemented, leader election guarantee that all nodes in the cluster know which one is the leader at any given time and can elect a new leader if the leader dies for whatever reason.

Often used when you want to perform an operation only once like a payment and do not do duplicate payments in a third party services where you can't have access to their system.

A leader election is a way to add redundancy to our system where just one server is the responsable to perform all operations.

## Consensus Algorithm

A type of complex algorithms used to have multiple entities agree on a single data value, like who the leader is amongst a group of machines. Two popular consensus algorithms are:
- Paxos
- Raft

They are extremely difficult to implement. So, when you want to use leader election you can use third party services.





## Paxos & Raft

Two consensus algorithms that, when implemented correctly, allow for the syncronization of certain operations, even in a distributed system.

## Etcd

Etcd is a strongly consistent and highly available key-value store that's often used to implement leader election in a system.

https://etcd.io

## ZooKeoper

Zookeeper is a strongly consistent, highly available key-value store. It's often used to store important configuration or to perform leader election.

https://zookeeper.apache.org

These data stores of key-value are highly available and strongly consistent. They will never give you a different answer of two request at the same time or state data. 

In a nutshel, you will have in your system multple servers comunicating by etcd using the key value store and any given point in time you will have one special key value pair would represent who is the leader among the server. The key is the leader or leader representation and value name of your server or the IP of your server desintate to be the leader. At any point in time the key-value pair is correct.

``` python
import etcd3

Leader_key = "flyland/leader"

etcd3.cleint() # initialize the client

while True:
    is_leader, lease = .... # this function returns if the current client is the leader
    if is_leader:
        print("I'm the leader")
    else:
        wait_for_next_election(client)
```

You can check how to use it in the documentation and Clements explain this very well.