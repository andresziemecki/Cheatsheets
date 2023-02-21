# Logging and Monitoring

## Logging

The act of collecting and storing logs--useful information about events in your system. Typically your program will output log messages to its STDOUT or STDERR pipes, which will atuomatically get aggregated into a **centralized logging solution**.

You would like to have as much information as possible in your logs. So, choosing a right format is important here. One format could be SYS and another one JSON. Then you can use stack driver from Google to collect this logs and store them into a database.

TO store the logging, it is used a time series database and your system periodically send metrics to this database. Then you can query this database and make charts. 

## Monitoring

The progress of having visibility into a system's key metrics. Monitoring is typically implemented by collecting important events and aggregated them into a human-readable charts.

## Alerting

The process through which system administrators get notified when critical system issues occur. Alerting can be set up by defining specific thresholds on monitoring charts, past which alerts are sent to a channel communication like Slack.