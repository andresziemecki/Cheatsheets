# Latency and Throughput

Two important measures of a system. Accuracy (How accurate is the data provided) and uptime (how much time is up and running vs total time) are another two measures in a system.

These measurement are not correlated, if there is high latency doesn-t mean it will have high throughput.

## Latency

The times it takes to a certain operation to complete in a system (for example, for the client to the server and then from the server to the client). We can also split the total latency in sublatency and measure each part. Most often this measure is a time duration, like milliseconds or seconds. You should know these orders of magnitude:

- Reading 1MB from RAM: 0.25ms
- Reading 1MB from SSD: 1ms
- Transfer 1MB over network of 1Gbps (One Giga Bit per second) is 10ms.
- Reading 1MB from HDD: 20ms
- Inter Continental Round trip: 150ms

## Throughput

The number of operations that a system can handle properly per time unit. For instance the throughput of a server can often be measured in request per seconds (RPS or QPS). Typically we measure throughput in Gbps or Mbps. In other words, how many request per second and at the same time the request can be converted into bit and then you get how many bit per seconds you have for throughput.
