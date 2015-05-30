## Hive Basics

### Install Hive on OSX

1. Install mysql, hive

[Installiation Guide](https://ravikkaushik.wordpress.com/2014/02/15/install_hive_mac_osx-10-9/)

- set `$HIVE_HOME`, `HCAT_HOME`
- download [Mysql JDBC Connector](http://dev.mysql.com/downloads/connector/j/)
- copy connector into `$HIVE_HOME/lib/hive`

2. create metastore db in mysql

```mysql
mysql> CREATE DATABASE metastore_db;

mysql> CREATE USER 'hiveuser'@'%' IDENTIFIED BY 'hivepassword';

mysql> GRANT all on *.* to 'hiveuser'@localhost identified by 'hivepassword';
```

3. Create `$HIVE_HOME/conf/hive-site.xml`

[datanucleus.autoCreateTables Issue](http://blog.163.com/renjianqin_1984/blog/static/1328821542012111410312962)

```xml
<configuration>
  <property>
    <name>fs.default.name</name>
    <value>hdfs://127.0.0.1:9000</value>
  </property>

  <property>
    <name>javax.jdo.option.ConnectionURL</name>
    <value>jdbc:mysql://localhost:3306/metastore_db?createDatabaseIfNotExist=true</value>
  </property>

  <property>
    <name>javax.jdo.option.ConnectionDriverName</name>
    <value>com.mysql.jdbc.Driver</value>
  </property>

  <property>
    <name>javax.jdo.option.ConnectionUserName</name>
    <value>hiveuser</value>
  </property>

  <property>
    <name>javax.jdo.option.ConnectionPassword</name>
    <value>hivepassword</value>
  </property>

  <property>
    <name>hive.metastore.uris</name>
    <value>thrift://127.0.0.1:9083</value>
    <description>IP address (or fully-qualified domain name) and port of the metastore host</description>
  </property>

  <property>
    <name>datanucleus.autoCreateTables</name>
    <value>true</value>
  </property>

  <property>
    <name>datanucleus.autoCreateColumns</name>
    <value>true</value>
  </property>

</configuration>
```
ALTER DATABASE metastore_db character set latin1;

4. Run hive

disable hadoop safe mode

```shell
hadoop dfsadmin -safemode leave
```

```shell
$ hive --service metastore &
$ hive
```

5. Trouble Shooting

[Create Table: Key was too long Issue](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_dataintegration/content/ch_using-hive-troubleshooting.html)

```
An exception was thrown while adding/validating classes) : Specified key was too long; max key length is 767 bytes
```

Change table char-set

```mysql
mysql> ALTER DATABASE <metastore_database_name> character set latin1;
```

### Hive

![](http://hortonworks.com/wp-content/uploads/2013/10/hadoopstack.png)

![](http://image.slidesharecdn.com/integrationofapachehiveandhbasefinal-120504182226-phpapp02/95/integration-of-hive-and-hbase-5-728.jpg?cb=1336174216)

### What Is Hive

Hive is a data warehousing infrastructure based on Hadoop. Hadoop provides massive scale out and fault tolerance capabilities for data storage and processing using MR

Hive is designed to enable easy data summarization, ad-hoc querying and analysis of large volumes of data. It provides a simple query language called **Hive QL**, which is based on SQL and which enables users familiar with SQL to do ad-hoc querying, summarization and dat analysis easily.

### What Hive Is NOT

Hadoop is a batch processing system and Hadoop jobs tend to have high altency and incur substantial overheads in job submission and scheduling. As a result, latency for Hive queries is generally very high (minutes) even when data sets involved are very small. Hive aims to provide acceptable (but not optimal) latency for interactive data browsing, queries over small data sets or test queries.

Hive is **not designed for online transaction processing** and **doesn't offer real-time queries and row level updates**. It is best used for batch jobs over large sets of immutable data (like web logs).


### Getting Started

[Apache: Hive Getting Started](https://cwiki.apache.org/confluence/display/Hive/GettingStarted#GettingStarted-Hive,Map-ReduceandLocal-Mode#GettingStarted-DDLOperations)

[Apache: Hive Tutorial](https://cwiki.apache.org/confluence/display/Hive/Tutorial)
