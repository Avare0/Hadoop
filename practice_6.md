# Урок 6. NoSQL в Hadoop. Hbase/Cassandra
1. Модифицировать свой Flume-фгент, созданный в предыдущем ДЗ таким образом, чтобы данные попадали в HDFS и Hbase одновременно
```
Name the components on this agent
flume5_9.sources = s1
flume5_9.sinks = k1 k2
flume5_9.channels = c1 c2

Describe/configure the source
flume5_9.sources.s1.type = exec
flume5_9.sources.s1.command = tail -f /tmp/data.txt

Describe the sink
flume5_9.sinks.k1.type = hdfs
flume5_9.sinks.k1.hdfs.path = /flume/student5_9/

flume5_9.sinks.k2.type = org.apache.flume.sink.hbase.HBaseSink
flume5_9.sinks.k2.table = student5_9
flume5_9.sinks.k2.columnFamily = info

Use a channel which buffers events in memory
flume5_9.channels.c1.type = memory
flume5_9.channels.c1.capacity = 1000
flume5_9.channels.c1.transactionCapacity = 100
flume5_9.channels.c2.type = memory
flume5_9.channels.c2.capacity = 1000
flume5_9.channels.c2.transactionCapacity = 100

Bind the source and sink to the channel
flume5_9.sources.s1.channels = c1 c2
flume5_9.sinks.k1.channel = c1
flume5_9.sinks.k2.channel = c2
```

![](https://imgur.com/3XZFaEh.png)
