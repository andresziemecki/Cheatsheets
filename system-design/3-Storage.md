# Storage

## Databases

Databases are programs that either use disk or memory to do 2 core things: record data and query data. In general, they are themselves servers that are long lived and interact with the rest of your application through network calls, with protocols on top of TCP or even HTTP.

Some database only keep records in memory, and the users of such databases are aware of the fact that those records may be lost forever if the machine or process dies.

For the most part though, databases needs persistance of those records, and thus cannot use memory. This means that you have to write your data to disk. Anything written to disk will remain through power loss or network partitions, so that's what it used to keep permanent records.

Since machine die often in a large scale system, special disk partitions or volumenes are used by the database processes, and these volumnes can get recovered even if the machine were to go down permanently.

## Disk

Usually refers to either HDD (hard-disk drive) or SSD (solid-state drive). Data written to disk will persist through power failures and general machine crashes. Disk is also referred to as non-volatile storage.

SSD is far faster than HDD, but also far more expensive from a financial point of view. Because of that, HDD will typically be used for data that's rarerly accessed or updated, but that's stored for a long time, an SSD will be used for data that is frequently accessed and updated.

## Memory

Short for Random Access Memory (RAM). Data stored in memory will be lost when the process that has written that data dies.

## Persistent Storage

Usually refers to disk, but it refers to any form of storage that persist if the process in charge of managing it dies.

## Distribute storage

Store data in multiple machine to atack different problems, like consistency por example. When we try to solve those problems, then a question may arise with your implementation: Are you going to get staleless data or the last updated one?
