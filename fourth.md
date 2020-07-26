# Урок 4. Заливка данных в Hadoop. Форматы хранения файлов

1. Создать две таблицы в форматах PARQUET/ORC/AVRO c компрессией и без оной.
```
drop table data;
drop table data_comp;
create table data
stored as ORC 
TBLPROPERTIES ("orc.compress"="NONE")
AS select * from hive_db.citation_data;
create table data_comp
stored as ORC 
TBLPROPERTIES ("orc.compress"="SNAPPY")
AS select * from hive_db.citation_data;
```
2. Верифицировать способ сжатия при помощи parquet-tools/avro-tools/hive --orcfiledump
![](https://i.imgur.com/TaeUHnU.png)
3. Посмотреть на получившийся размер данных.
![](https://imgur.com/XsMhYcv.png)
4. Сделать выводы о эффективности хранения и сжатия.
**Данные сжались практически в 3 раза**
