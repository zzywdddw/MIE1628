# LEC 1  
### Types of Big Data
1. Structured: Organised data format with a fixed schema. Ex: RDBMS, CSV, XLS
2. Semi-Structured/Multi Structured: Partially organized data which does not have a fixed format. Ex: XML, JSON, DOC
3. Unstructured: Unorganized data with an unknown schema. Ex: Audio, video files, jpg etc.

### Big Data: 3V’s
<strong>Volume</strong>(scale); Ex: CERN’s LHC generates 15 PB a year  
<strong>Velocity</strong>(speed); Ex: Data is generated fast and need to be processed fast. Healthcare Monitoring: Sensors monitoring your activities and body for any abnormal measurements that require immediate action.  
<strong>Variety</strong>(complexity); Ex: A single application can be generating/collecting
many types of data  

### Big Data: 3V’s + 1
Veracity: uncertainty due to data inconsistency and incompleteness  
And more V's  
<br>

![image](https://github.com/user-attachments/assets/a430c6df-215c-4316-9560-fcc9a231573c)

### Types of Databases  
- Relational Databases: SQL Server, PostgreSQL, SQLite, MySQL, Azure SQL
- Non-relational Databases: Azure Cosmos DB
- Cloud Databases: Any data that is run in a cloud using IAAS, DAAS, PAAS
<br>
<br>

# LEC 2  Part1：Hadoop Ecosystem Major Components
### HDFS  
HDFS- Hadoop Distributed File System  
HDFS 是 Hadoop 核心组件之一，是一个高容错、低成本、适用于大数据存储的分布式文件系统。  
### YARN  
YARN - Yet Another Resource Negotiator  
YARN is the resource management and job scheduling technology  
Responsible for allocating system resources to various application running in a Hadoop cluster and scheduling tasks to be executed on different cluster nodes.  
##### YARN Components  
 • Resource Manager: Runs on a master daemon and manages the resource allocation in the cluster.  
 
 • Node Manager: They run on the slave daemons and are responsible for the execution of a task on every single Data Node.  
 
 • Application Master: Manages the user job lifecycle and resource needs of individual applications. It works along with the Node Manager and monitors the execution of tasks.  
 
 • Container: Package of resources including RAM, CPU, Network, HDD etc. on a 
single node.  
![image](https://github.com/user-attachments/assets/b606a11f-a562-468c-92aa-ee4e5548349d)  
### MapReduce  
MapReduce 是一种编程模型和相应的实现，用于处理和生成大型数据集。  
用户定义一个 map 函数，这个函数处理一个键/值对（key/value pair），生成一组中间的键/值对。还需要定义一个 reduce 函数，它会把所有具有相同中间 key 的值合并在一起。合并成最终输出。  
<br>
<br>  
### Apache Hadoop Ecosystem  

![image](https://github.com/user-attachments/assets/e672b22a-f67a-4105-bff9-4c7839b14511)  


### Apache Sqoop  
用于高效地在 Apache Hadoop 和结构化数据存储（如关系型数据库）之间传输大量数据。  
Ex:假设你有一个 MySQL 数据库，里面有一张几百万行的订单表，你想把它导入到 Hadoop 中进行大数据分析,用 Sqoop 一条命令就可以做到：  
```
sqoop import \
  --connect jdbc:mysql://localhost/salesdb \
  --table orders \
  --username root --password 123456 \
  --target-dir /user/hadoop/orders
```
### Flume  
- 用于高效地收集、聚合和传输大量日志数据。比如用来实时接收来自服务器、网站、应用的日志（log）或事件数据
- Flume 基于流式数据流（streaming data flows），Flume 非常稳定、具有容错性、可扩展性强
### Hive  
Hive 是一个面向 Hadoop 的分布式数据管理系统，让用户用熟悉的 SQL 查询语言来分析大数据，适合做大规模的数据提取、分析和挖掘。  
### Oozie  
Oozie 是管理 Hadoop 作业的“任务调度器”，用于定义、定时、自动执行多个大数据处理任务的工作流。  
### Zookeeper  
Zookeeper 就是一个中心化的 Key-Value 存储系统，供分布式系统各组件之间协调和通信。  
- 比如多个服务要“抢占一个任务”，Zookeeper 可以提供一个“锁”，谁先拿到就先做任务
- 它本身也必须运行在多个机器上（集群），保证自己不会挂掉
### HBase  
HBase 是 Hadoop 上的一个面向列的、分布式 NoSQL 数据库，擅长处理海量数据的高效读写，适合实时访问大数据。  
### Apache Cassandra  
Cassandra 是一个去中心化的、高可用、高可扩展的分布式 NoSQL 数据库，专门用于处理海量数据并避免单点故障。  
# LEC 2  Part2：Hadoop Design Goals  
### Moving Computation to Data  
Hadoop 背后的核心思想是：与其把数据移动到计算节点，不如把计算逻辑移动到存储数据的节点上。  
- 在传统系统中：数据通常会被传送到计算服务器 → 慢 & 成本高  
- 在 Hadoop 中：数据存在哪里，计算就在哪里执行 → 节省带宽、提升效率
- 这就是所谓的“计算向数据靠拢”原则（data locality）
### Scalability， Scaling， Reliability  
### New Approach to Data : Keep all the Data  
新时代的大数据理念是“保留一切数据”，通过灵活的读取方式和更丰富的分析，利用细粒度数据获得更优的洞察和结果。  
# LEC 2  Part3：Hadoop Distributed File System









  
