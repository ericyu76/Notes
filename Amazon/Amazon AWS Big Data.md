# Amazon AWS Big Data

Most attendees are 媒體，B2C...

**ask question is the data mining**

Retail 常見的應用

*   Recommendations
*   Transaction Analysis

大部分的Big Data 使用者只用在很簡單的統計分析，少數像 netflix 的公司有 data scintise.

**Apache Hadoop**

*   簡化 Cluster 的佈署
*   處理未知問題，資料多變性，大量資料
*   Supports SQL and Others

**Hadoop Core Modules**

*   HDFS (Hadoop Distribued File System)
*   YARN (yet resource negociated)
*   MapReduce: YARN-based, Java Programming Framework
*   Hive: SQL like query
*   Impala: SQL like query (real time query)
*   Pig: Programming in (Pig Latin)
*   Mathout: Machine Learning
*   HBase: non-releational data store
*   Spark: in-memory data analysis
*   Spark SQL
*   Ganglia: Monitoring framework 

**Amazon EMR(Elastic MapReduce) vs Hadoop**

Total cost is lower then on-premises

*   on-demend
*   spot instance: bid price (may lower)

**AWS Market place - BigData**

[](https://aws.amazon.com/marketplace/ref=brs_navhdr_header)https://aws.amazon.com/marketplace/ref=brs_navhdr_header

## Amazon EMR hadoop 1.x

*   Master Node

        *   Job Tracker
    *   Name Node(對外服務?)
    *   Hive
    *   Pig

*   Core Node(multiple)

        *   TaskTracker
    *   Data Node
    *   HDFS

**EMR Master Node (maps to Hadoop master node)**

*   only one master node
*   Run JobTracker, NameNode
*   Coordinates MapReduce task

**EMR core Nodes**

*   use instance storage attach
*   未來也可以用 EBS
*   Master Node管理，幾乎不用碰到它

**EMR Task Nodes(maps to Hadoop slave node)**

*   managed by master node, too

## Amazon EMR Hadoop 2.x (YARN)

[](https://hadoop.apache.org/docs/r2.4.1/hadoop-yarn/hadoop-yarn-site/YARN.html)https://hadoop.apache.org/docs/r2.4.1/hadoop-yarn/hadoop-yarn-site/YARN.html

Master Node

*   Resource Manager(manage with Node Manager)
*   Name Node (work with Data Node)

Core node

*   Node Manager
*   Data Node

Task Node

*   Node Manager

**Lab**

*   [](https://evantage.gilmoreglobal.com/#/books)https://evantage.gilmoreglobal.com/#/books

        *   eric.yu@testriegroup.com/ping5678

*   [](https://awstraining.csod.com/client/awstraining/default.aspx)https://awstraining.csod.com/client/awstraining/default.aspx

        *   ericyu76/Ping1234

**Amazon MapReduce**

Map (key-values) --> Shuffle --> Reduce (加總或排序)

**EMR Cluster **

*   Transient

        *   cluster 會 terminate
    *   臨時使用, HDFS 會刪掉
    *   10 nodes for 10 hour = 100 nodes for 1 hour (Cost)

**Configuraion**

**   Setps

**EMR save output to Amazon S3**

*   Output Format- Text with key value, OutputFormat interface to Customized, SerDe (serializer
*   S3 can be compressed

**Lab 1**

1.  create EMR (will create ec2 as well)
2.  create S3 for storing input and output
3.  Run pig

*   MapReduce the data

1.  run pig in grunt shell
2.  run pig in pig batch file using steps

*   Resize the cluster

## Programming

**High Level**

*   **Apache Hive**

*   **Impala**

*   **Apache Pig**

**Low Level**

*   **Java MapReduce APIs**

        *   using Java classes to build
    *   YARN web service interface

**Other Libraries**

*   Mahout

        *   Machine Learning 
    *   Usefull for **Clustering** and **Classification**

**Hue**

*   Opensource web based GUI
*   [](http://gethue.com)http://gethue.com
*   EMR 可以用來 Metastore Manager, Job Browser (Hadoop jobs), User Management, AWS Samples

## Lab2 Using Hive

1.  建立 s3 bucket
2.  CREATE EXTERNAL TABLE from s3 sample

        1.  EXTERNALE 表示不在 S3 bucket
    2.  table 存在 Hive meta store (不能改變 location)
    3.  可以在不同的 cluster 去 join table

3.  執行 hive 加上 -d 可以設定變數，例如 SAMPLE/OUTPUT
4.  create table 加上 location 可以把結果放在 output(S3) 裡面

        1.  CREATE Table 似乎只是把資料動態 mapping 為 DB 的 table
    2.  將 table 儲存到 S3:

                1.  CREATE EXTERNAL TABLE joined_impressions (requestBeginTime string, adId string, impressionId string, referrer string, userAgent string, userCookie string, ip string, clicked Boolean) PARTITIONED BY (day string, hour string) STORED AS SEQUENCEFILE **LOCATION '${OUTPUT}/tables/joined_impressions'**;

5.  使用 partition table 來讓存取速度變快
6.  RECOVER PARTITION 的目的為何, Hive 建立 partition 來加速存取的速度

## Moduel 5: Spark and Spark SQL (in memory analytics)

**Spark (**[](http://spark.apache.org))**[http://spark.apache.org](http://spark.apache.org/))**

＊使用 memory 來改善 Map reduce 與 HDFS/S3 之間 IO的速度

＊支援 HDFB, HBase, Sequence Files, Amazon S3

*   進行 BI 速度很快，可以用來產生 tableau, Jasper Report
*   **建議優先考慮 Spark 來進行 BigData**

**Spark SQL**

*   比論為 Hive on Spark - 使用 spark取代 MapReduce
*   In memory 比 Hive 快100倍, On Disk 比 Hive 快10倍
*   相容於 Hive 的 data, metastores, querys, user-defined function

**Shark - New name **equals **Spark SQL**

**Spark Programming Model**

*   Resilient  distributed datasets (RDDs)
*   map, filter, group by, join count, reduce, ...

**使用 Amazon 來使用 spark**

*   便宜
*   可以使用 RDDs 在 S3

## Lab 3 利用 python (streaming)

使用 python sdf file - 很大的分析檔案

*   s3://ap-northeast-1-aws-training/awsu-ilt/big-data/v1.7/data/lab3/data/substance-small.sdf

MapReducer

*   Map

        *   -mapper s3://ap-northeast-1-aws-training/awsu-ilt/big-data/v1.7/data/lab3/scripts/calculateMolecularWeight.py 

## Lab 4 Spark

瀏覽 s3 bucket  的方式

*   >aws s3 ls s3://xxxx

## Amazon EMR Cost

Cost in serval 

1.  EMR

        1.  EMR upcharge
    2.  EC2 instances 

                1.  On-demand
        2.  Reserved (1-3 years)
        3.  Spot (不適合用在 Master/Core node, 若價格超過定價，會關掉 instance)

2.  Data Storage

        1.  S3 (相對便宜) [](http://aws.amazon.com/tw/govcloud-us/pricing/s3/)[http://aws.amazon.com/tw/govcloud-us/pricing/s3/](http://aws.amazon.com/tw/govcloud-us/pricing/s3/)

                1.  storage GB-Month, request
        2.  可以有 7 個 9 的 availiability
        3.  RRS 更便宜，但只有 4 個 9的 availiablity

        2.  Redshift
    3.  DynamoDB
    4.  RDS

## EMR Security

master security group (不要給人家碰到)

slave security group

## Module 8 Data Ingestion, Transfer, Compression

**Data Ingestion (拮取)**

*   Amazon 使用 **Apache Flume**
*   Amazon Kinesis - streaming 的方法取得 Big data 及處理
*   Open Source - Apache Kafka

**Data Transfer**

*   Direct Connect － direct link to Corpation Data Center, 802.1q VLANs
*   VPN Connection
*   Amazon S3 multipart upload (API)
*   AWS import/export - 使用移動式硬碟

使用 **Apache Sqoop** 來進行 transfer 資料, 也有其他方式，可以在 market place 上面找第三方的 AMI

**Data Compression**

## Module 9 Kinesis to near Real-Time

**幾種處理資料的方式**

*   Query Engine - Data Warehouse, NoSql DB, Repeat Query
*   Batch Engines - MapReduce
*   Streaming big data － Amazon Kinesis/Apache Kafka

        *   例如：遊戲軟體若使用者使頻率愈來愈低，就不玩了。可以突然給個寶物強化物機

*   String (ingest) tools convert random streams in to sequential steams

google awslabs 可以找到一些說明

Data producer 使用 PUT 把資料送進 Kinessis

Data Consumer 再把資料從 Kinessis 把資料帶走

## Lab 5 Kinesis

**Overview**

*   Stream 資料從 EC2 windows, Log4j 送至 Kinesis
*   Kinesis 再把資料送至 EMR 再送給 Hive 進行分析

## Module 10 Storage

**DynamoDB (NoSQL with full managed)**

*   有最低的 latency, 用在 hot data
*   no fixed schema
*   run on SSD
*   Region scoped
*   Integration with EMR

**Amazon RDS**

*   Structured Data
*   Oracle, Mysql, SQLServer, Aurora(Mysql like, multi-nodes)
*   Using Apache Sqoops to import/export data

**Amazon Redshift**

*   用在 Warehouse
*   Petabyte-scale database

        *   Columnar storage
    *   Massively parall

*   Complex SQL

**Amazon EMR(HDFS)**

*   HDFS(local disk)
*   node 上的資料不是永久保存的，使用 S3 來儲存結果

**Amazon S3 (for unstructure, hot data)**

**Amazon Glacier**

*   極低的成本
*   適用在 Archived的資料 (cold data)

![](https://hackpad-attachments.s3.amazonaws.com/hackpad.com_PD86Jq5t0u7_p.236988_1433474563884_factor.jpg)

![](https://hackpad-attachments.s3.amazonaws.com/hackpad.com_PD86Jq5t0u7_p.236988_1433474820013_factor2.jpg)

## Lab 6 DynamoDB

1.  建立 DynamoDB Table (primary key)
2.  透過 EMR 的 Hive, 把資料從 S3 把資料轉到 DynamoDB
3.  再透過Hive 把 DynamoDB 資料再轉回 Hive

心得

1. BigData 主要的運算及計算，透過 Hadoop 的 MapReduce(Maper and Reducer) 來進行

*   有三種 node
*   利用 HDFS 儲存資料 (暫時/永久)
*   可以使用 Hive, Pig ...

## Module 11 Redshift

**使用情境**

*   取代原來的 Data Warehouse Solution
*   可以使用 SQL(真的 SQL, 不是 Hive 那種 SQL-Like),  可以用 ODBC, JDBC 連接
*   較便宜

**Use Case**

1.  一般來說 OLTP 接在 DynamoDB， Redshift 再接在 DynamoDB 後面

**Hive vs Redshift**

*   Hive is not true SQL, Hive handle non-structure/semi-structured
*   Redshift Need Structured Data - 需要 ETL (Transformation)
*   需要較複雜的 SQL 時，可以使用 Redshift

**Columnar Storage reduces I/O**

*   Row base read every row to get certern column
*   Column base read column only (效能較佳)

**Compress Data**

Data Warehouse 有時 CPU 比記憶體閒

**Redshift Architect**

*   Leader Node (與 SQL Clients/BI Tools 連接)
*   Compute nodes

        *   暫時不用的資料可以 hibernate 到 S3/DynamoDB, 需要時再 restore 回來

*   也有 Single node version

## Lab 7 Redshift

*   aws s3 cp 可以 copy
*   使用 hdfs:// 來暫存處理的資料，最後要記得存回 S3
*   RLIKE 來移除不要的資料
*   Redshift 是把 PostgresSQL 再拿去改，可以用 PostgresSQL 的 Client(JDBC/ODBC)
*   但 Redshift 是 Column Based 的 storage

## Module 12 Visualization & Orchestrate

Business Analysts 沒辦法寫 Hive....

**工具**

*   Tableau

        *   可以使用 EMR

*   Jaspersoft (Tibico)

        *   可以在 market place 裡找到很便宜的 image
    *   支援 EMR, RDS

**Visualzation 與工具的關係**

*   **Hive**

*   **Impala**

*   **HDFS**

*   **DynamoDB**

*   **Kiness**

*   **Redshift, RDS**

**AWS Data Pipeline**

*   data driven workflow

        *   資料轉來轉去有點複雜，我們需要一個工具來管理
    *   **Big Data 資料轉換的工作流工具**

*   支援所有 Amazon的 storage
*   Failure monitor/Notification
*   Components

        *   Input Datanode
    *   Activity
    *   Output Datanode

*   Definetion

        *   有點複雜 (Activity - Pre-condition, actions...)

*   Scheduling

**_Apache Oozie_**

*   Open Source Solution
*   Can be a bootstrap step in EMR

## Lab 8 Visualization