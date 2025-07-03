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
### Scalability， Reliability  
### New Approach to Data : Keep all the Data  
新时代的大数据理念是“保留一切数据”，通过灵活的读取方式和更丰富的分析，利用细粒度数据获得更优的洞察和结果。  
# LEC 2  Part3：Hadoop Distributed File System  
### What is Hadoop?  
- Hadoop is a framework that allows you to store large volume of data on several node machines
- Hadoop also helps in processing data in a parallel manner
### What is HDFS?  
- HDFS is the storage layer of Hadoop that stores data in multiple data servers
- Data is divided into multiple blocks and Stores them over multiple nodes of cluster
### HDFS Blocks  
一个block可以存128MB的数据。 Ex：一个380MB的文件会被存到3个Block里，分别是Block1（128MB),Block2（128MB), Block3（124MB)  
### NameNodeand DataNode  
NameNode（主节点 / 元数据管理器）:  
- 负责管理和协调所有 DataNode并且保存所有元数据，包括：
   1. 文件被切成了哪些 block
   2. 每个 block 存在哪些 DataNode 上
   3. 文件大小、访问权限、目录结构等信息
- 定期接收所有 DataNode 发来的：
   1. 心跳（heartbeat）：确认节点是否在线
   2. Block 报告：告知当前节点有哪些数据块
 
DataNode（从节点 / 数据存储者）
- 真正存储数据块（block）的地方。
- 客户端读取文件 → DataNode 返回对应的数据块
- 客户端上传文件 → DataNode 接收并存储分配的块
# LEC 2  Part4：Hadoop MapReduce  
### Intro  
MapReduce 是一种编程模型及其实现，用于处理和生成大规模数据集。  
用户定义一个 map 函数来处理键/值对，生成中间的键/值对，再通过 reduce 函数对相同键的中间值进行合并。  
- Map 阶段：处理输入数据，生成中间结果：

  例子：("doc1", "hello world") → [("hello", 1), ("world", 1)]

- Reduce 阶段：聚合相同 key 的值：

  例子：("hello", [1,1,1]) → ("hello", 3)
  <br>
![image](https://github.com/user-attachments/assets/a555b396-cb9f-4e2a-bfe2-08807df80783)
![image](https://github.com/user-attachments/assets/ba55ce90-f057-4015-adc9-2696ee34e9bf)
<br>

# LEC 3  
### Intro  
传统 MapReduce 的执行流程：Map → Shuffle → Reduce. 每一步之间必须将中间结果写入磁盘以实现容错. 这就导致了：I/O 成本高(写磁盘慢), 性能低下, 系统不够灵活  

RDD（Resilient Distributed Dataset） 是 Spark 的最底层编程模型。它是一种 弹性分布式数据集，支持 容错、并行计算 和 分布式内存存储。  
![image](https://github.com/user-attachments/assets/2daded20-a11e-434c-bb96-6d2c829be4af)  
### RDD,Spark,Hadoop的关系  
- Hadoop 是最早的大数据平台,包含两个核心组件：
    - HDFS：分布式文件系统，用来存储大数据
    - MapReduce：分布式计算模型，执行慢，每一步都写磁盘
    - 缺点：写磁盘太频繁，开发复杂，速度
- Spark 是对 Hadoop MapReduce 的改进. Spark 是一个 通用的分布式计算框架, 它可以直接：
    - 读取 HDFS 中的数据
    - 也能在 Hadoop YARN 上运行任务
    - 优势：把中间结果放到内存里（不像 MapReduce 写磁盘）; 支持批处理、流处理、机器学习等各种任务
- RDD 是 Spark 的核心数据抽象

### DAG  
DAG stands for Directed Acyclic Graph.  
DAG 就是 Spark 在背后画的一张“任务流程图”，让代码能高效、有顺序、不会出错地在多个机器上执行。
```
from pyspark import SparkContext

sc = SparkContext("local", "DAG Example")

# Stage 0: parallelize + subtract input
rddA = sc.parallelize([1, 2, 3, 4])      # parallelize A

# Stage 1: another parallelize + transformations
rddB = sc.parallelize([3, 4, 5, 6])      # parallelize B
rddB_mapped = rddB.map(lambda x: x * 2) # map
rddB_flat = rddB_mapped.flatMap(lambda x: [x, x + 1]) # flatMap

# Stage 2: subtract between two RDDs
result = rddA.subtract(rddB_flat)

# Trigger execution
print(result.collect())
```
![image](https://github.com/user-attachments/assets/7b93e5fb-36fa-402e-8ca0-b2bf785fce56)  
<br>
<br>

# LEC 4  Part1：Recommendation system  
### Types of Recommendation system  
![image](https://github.com/user-attachments/assets/f77a8103-c1be-402d-9ef7-953a360ae62e)  
![image](https://github.com/user-attachments/assets/b1a1e1ba-df15-4958-bd3b-b80e184ff0fc)  
### ALS  
Alternating Least Squares（ALS，交替最小二乘法）  
![image](https://github.com/user-attachments/assets/18b63642-4cce-4b91-a5e7-36c757c523cf)  
左图：原始评分矩阵（很多空缺）， 很多格子是 BLANK（未知），表示用户没看过或没打分。目标：用 ALS 算法 填补这些空缺，即预测评分。  
![image](https://github.com/user-attachments/assets/327e9ffe-1dad-43a7-99f3-535867f996f6)  
1. 输入：评分矩阵 R（m × n）
     - 其中 m 是用户数量，n 是物品数量。
     - 大多数元素是缺失的（即未评分）。
2. 矩阵分解目标，将 R 分解成两个矩阵的乘积：
     - 用户矩阵 U（m × k）：每个用户在 k 个隐因子上的兴趣强度；
     - 物品矩阵 P（n × k）：每个物品在 k 个隐因子上的属性特征；
     - 所以：R ≈ U × Pᵗ。
3. 损失函数（目标函数）：
     - 第一项是预测误差；
     - 第二项是正则化，用于防止过拟合；
     - 只对已知评分 R_ij 做损失计算。
4. 交替优化（Alternating）：
     - 固定 P，优化 U（相当于解一个线性最小二乘问题）；
     - 然后固定 U，优化 P；
     - 不断交替，直到误差收敛。
<br>
<br>

# LEC 4  Part2：Databricks  
Databricks 是一个基于 Apache Spark 构建的云端数据分析平台。它把 Spark 封装在一个漂亮、易用的界面中，并添加了团队协作、云存储、机器学习等高级功能。  
简单的来说，Databricks = Spark + 云平台 + 可视化界面 + ML 工具 + 多语言支持 + 团队协作功能  
<br>
<br>

# LEC 5  Part1：Recommendation system  























  
