# Урок 5. Потоковая обработка данных. Flume/Flink/SparkStreaming
## Для части по SQOOP
1. Провести импорт таблицы из вашего сервера БД в Hadoop с использованием SQOOP в любых двух вариантах из перечисленных ниже.
a. в Hive-таблицу (--hive-import)
```
sqoop import --connect jdbc:postgresql://node3.novalocal/pg_db --username exporter -P --table character --hive-import --hive-database student5_9 --hive-table character
```
![](https://imgur.com/xc22WuX.png)
b. в HDFS в формате avro (--as-avrodatafile)
```
sqoop import --connect jdbc:postgresql://node3.novalocal/pg_db --table character --target-dir /student5_9/tables/ --as-avrodatafile --username exporter -P
```
## Для части по потоковой обработке (Flume)
1. Создать Flume-агент с именем, соответствующим имени своего пользователя (например Flume4_20)
2. Создать любой Flume поток используя Flume сервис соответствующего номера.
• Тип источника источник – exeс
• Тип канала – memory
• Тип слива – hdfs

```
flume5_9.sources = s1
flume5_9.sinks = k1
flume5_9.channels = c1

flume5_9.sources.s1.type = exec
flume5_9.sources.s1.command = tail -f /tmp/data.txt

flume5_9.sinks.k1.type = hdfs
flume5_9.sinks.k1.hdfs.path = /flume/student5_9/

flume5_9.channels.c1.type = memory
flume5_9.channels.c1.capacity = 1000
flume5_9.channels.c1.transactionCapacity = 100

flume5_9.sources.s1.channels = c1
flume5_9.sinks.k1.channel = c1
```

![](https://imgur.com/ISjo0Ve.png)

3. Создать поверх данных в hdfs таблицу через которую можно просмотреть полученные данные.
```
create external table les_6 
(text string)
stored as sequencefile
location '/flume/student5_9/'
```
```
select * from les_6;
```

