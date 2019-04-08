---
headless: true
---

# 交通大数据应用研究

##  什么是大数据？

- 大数据就是多，就是多。原来的设备存不下、算不动。————啪菠萝·毕加索
- 大数据，不是随机样本，而是所有数据；不是精确性，而是混杂性；不是因果关系，而是相关关系。————Schönberger
- 大数据是大数据的采集。

大数据最根本之处在于信息收集方式出现了重大变化与革新。大数据的出现与大量信息直接在网络呈现关系非常紧密。

![](/images/bigdata01.png)

微博、天猫、淘宝、微信等等都直接产生了大量包括定位、消息记录、消费记录、评价、阅读等等极为庞大的信息，可以说互联网企业都自然的带有数据企业的标签。
不过如果我们从数据的源头看的更仔细一些，还是会发现，其实很多数据依然是有巨大的采集与归类的需求。

![](/images/bigdata02.png)

##  大数据工具集：Hadoop、Hive、Spark 

### 大数据存储

传统的文件系统是单机的，不能横跨不同的机器。HDFS（Hadoop Distributed FileSystem）的设计本质上是为了大量的数据能横跨成百上千台机器，但是你看到的是一个文件系统而不是很多文件系统。比如你说我要获取/hdfs/tmp/file1的数据，你引用的是一个文件路径，但是实际的数据存放在很多不同的机器上。你作为用户，不需要知道这些，就好比在单机上你不关心文件分散在什么磁道什么扇区一样。HDFS为你管理这些数据。

### 大数据处理

这就是MapReduce / Tez / Spark的功能。MapReduce是第一代计算引擎，Tez和Spark是第二代。MapReduce的设计，采用了很简化的计算模型，只有Map和Reduce两个计算过程（中间用Shuffle串联），用这个模型，已经可以处理大数据领域很大一部分问题了。

Map＋Reduce的简单模型很黄很暴力，虽然好用，但是很笨重。第二代的Tez和Spark除了内存Cache之类的新feature，本质上来说，是让Map/Reduce模型更通用，让Map和Reduce之间的界限更模糊，数据交换更灵活，更少的磁盘读写，以便更方便地描述复杂算法，取得更高的吞吐量。

Pig是接近脚本方式去描述MapReduce，Hive则用的是SQL。它们把脚本和SQL语言翻译成MapReduce程序，丢给计算引擎去计算，而你就从繁琐的MapReduce程序中解脱出来，用更简单更直观的语言去写程序了。

Impala，Presto，Drill的诞生，解决了Hive在MapReduce速度慢的问题。这些系统让用户更快速地处理SQL任务，牺牲了通用性稳定性等特性。如果说MapReduce是大砍刀，砍啥都不怕，那上面三个就是剔骨刀，灵巧锋利，但是不能搞太大太硬的东西。

Hive on Tez / Spark和SparkSQL的设计理念是，MapReduce慢，但是如果我用新一代通用计算引擎Tez或者Spark来跑SQL，那我就能跑的更快。

上面的介绍，基本就是一个数据仓库的构架了。底层HDFS，上面跑MapReduce／Tez／Spark，在上面跑Hive，Pig。或者HDFS上直接跑Impala，Drill，Presto。这解决了中低速数据处理的要求。

又一种计算模型被开发出来，这就是Streaming（流）计算。Storm是最流行的流计算平台。流计算很牛逼，基本无延迟，但是它的短处是，不灵活，你想要统计的东西必须预先知道，毕竟数据流过就没了，你没算的东西就无法补算了。因此它是个很好的东西，但是无法替代上面数据仓库和批处理系统。

还有一个有些独立的模块是KV Store，比如Cassandra，HBase，MongoDB以及很多很多很多很多其他的（多到无法想象）。

除此之外，还有一些更特制的系统／组件，比如Mahout是分布式机器学习库，Protobuf是数据交换的编码和库，ZooKeeper是高一致性的分布存取协同系统，等等。

Yarn是另外一个重要组件，调度系统。用来调度这么多乱七八糟的工具在同一个集群上运转，使他们有序工作。

### 另一种说法

大数据技术本质上无非解决4个核心问题。

- 存储，海量的数据怎样有效的存储？主要包括hdfs、Kafka；
- 计算，海量的数据怎样快速计算？主要包括MapReduce、Spark、Flink等；
- 查询，海量数据怎样快速查询？主要为Nosql和Olap，Nosql主要包括Hbase、 Cassandra 等，其中olap包括kylin、impla等，其中Nosql主要解决随机查询，Olap技术主要解决关联查询；
- 挖掘，海量数据怎样挖掘出隐藏的知识？也就是当前火热的机器学习和深度学习等技术，包括TensorFlow、caffe、mahout等；

####  Google三本秘籍

- 《Google file system》：论述了怎样借助普通机器有效的存储海量的大数据；
- 《Google MapReduce》：论述了怎样快速计算海量的数据；
- 《Google BigTable》：论述了怎样实现海量数据的快速查询；

####  apache三大法门

- hdfs解决大数据的存储问题。
- mapreduce解决大数据的计算问题。
- hbase解决大数据量的查询问题。

####  技术演进

Hadoop不断衍生和进化各种分支流派，其中最激烈的当属计算技术，其次是查询技术。存储技术基本无太多变化，hdfs一统天下。以下为大概的演进：

- 1，传统数据仓库派出了hive，pig、impla等SQL ON Hadoop的简易修炼秘籍；
- 2，伯克利派推出基于内力（内存）的《Spark》，意图解决所有大数据计算问题。
- 3，流式计算相关门派推出了SparkStreaming、Storm，S4等流式计算技术，能够实现数据一来就即时计算。
- 4，apache推出flink，想一统流计算和批量计算的修炼；

##  大数据图谱

![](/images/bigdata03.png)

- HBase：是一个高可靠性、高性能、面向列、可伸缩的分布式存储系统，利用HBase技术可在廉价PC Server上搭建起大规模结构化数据集群。
- Pig：Yahoo开发的，并行地执行数据流处理的引擎，它包含了一种脚本语言，称为Pig Latin，用来描述这些数据流。Pig Latin本身提供了许多传统的数据操作，同时允许用户自己开发一些自定义函数用来读取、处理和写数据。在LinkedIn也是大量使用。
- Hive：Facebook领导的一个数据仓库工具，可以将结构化的数据文件映射为一张数据库表，并提供完整的sql查询功能，可以将sql语句转换为MapReduce任务进行运行。其优点是学习成本低，可以通过类SQL语句快速实现简单的MapReduce统计。像一些data scientist 就可以直接查询，不需要学习其他编程接口。
- Cascading/Scalding：Cascading是Twitter收购的一个公司技术，主要是提供数据管道的一些抽象接口，然后又推出了基于Cascading的Scala版本就叫Scalding。Coursera是用Scalding作为MapReduce的编程接口放在Amazon的EMR运行。
- Zookeeper：一个分布式的，开放源码的分布式应用程序协调服务，是Google的Chubby一个开源的实现。
- Oozie：一个基于工作流引擎的开源框架。由Cloudera公司贡献给Apache的，它能够提供对Hadoop MapReduce和Pig Jobs的任务调度与协调。
- Azkaban: 跟上面很像，Linkedin开源的面向Hadoop的开源工作流系统，提供了类似于cron 的管理任务。
- Tez：Hortonworks主推的优化MapReduce执行引擎，与MapReduce相比较，Tez在性能方面更加出色。

##  Hadoop vs Spark

先看结论：

如果说，MapReduce是公认的分布式数据处理的低层次抽象，类似逻辑门电路中的与门，或门和非门，那么Spark的RDD就是分布式大数据处理的高层次抽象，类似逻辑电路中的编码器或译码器等。

RDD就是一个分布式的数据集合（Collection），对这个集合的任何操作都可以像函数式编程中操作内存中的集合一样直观、简便，但集合操作的实现确是在后台分解成一系列Task发送到几十台上百台服务器组成的集群上完成的。最近新推出的大数据处理框架Apache Flink也使用数据集（Data Set）和其上的操作作为编程模型的。

由RDD组成的有向无环图（DAG）的执行是调度程序将其生成物理计划并进行优化，然后在Spark集群上执行的。Spark还提供了一个类似于MapReduce的执行引擎，该引擎更多地使用内存，而不是磁盘，得到了更好的执行性能。

那么Spark解决了Hadoop的哪些问题呢？

- 抽象层次低，需要手工编写代码来完成，使用上难以上手。
  - =>基于RDD的抽象，实数据处理逻辑的代码非常简短。。
- 只提供两个操作，Map和Reduce，表达力欠缺。
  - =>提供很多转换和动作，很多基本操作如Join，GroupBy已经在RDD转换和动作中实现。
- 一个Job只有Map和Reduce两个阶段（Phase），复杂的计算需要大量的Job完成，Job之间的依赖关系是由开发者自己管理的。
  - =>一个Job可以包含RDD的多个转换操作，在调度时可以生成多个阶段（Stage），而且如果多个map操作的RDD的分区不变，是可以放在同一个Task中进行。
- 处理逻辑隐藏在代码细节中，没有整体逻辑
  - =>在Scala中，通过匿名函数和高阶函数，RDD的转换支持流式API，可以提供处理逻辑的整体视图。代码不包含具体操作的实现细节，逻辑更清晰。
- 中间结果也放在HDFS文件系统中
  - =>中间结果放在内存中，内存放不下了会写入本地磁盘，而不是HDFS。
- ReduceTask需要等待所有MapTask都完成后才可以开始
  - => 分区相同的转换构成流水线放在一个Task中运行，分区不同的转换需要Shuffle，被划分到不同的Stage中，需要等待前面的Stage完成后才可以开始。
- 时延高，只适用Batch数据处理，对于交互式数据处理，实时数据处理的支持不够
  - =>通过将流拆成小的batch提供Discretized Stream处理流数据。
- 对于迭代式数据处理性能比较差
  - =>通过在内存中缓存数据，提高迭代式计算的性能。

因此，Hadoop MapReduce会被新一代的大数据处理平台替代是技术发展的趋势，而在新一代的大数据处理平台中，Spark目前得到了最广泛的认可和支持，从参加Spark Summit 2014的厂商的各种基于Spark平台进行的开发就可以看出一二。

ref: https://www.zhihu.com/question/26568496 用心阁的回答。

##  大数据技术栈

![](/images/bigdata04.jpeg)

- a.蓝色部分，是Hadoop生态系统组件，黄色部分是Spark生态组件，虽然他们是两种不同的大数据处理框架，但它们不是互斥的，Spark与hadoop 中的MapReduce是一种相互共生的关系。Hadoop提供了Spark许多没有的功能，比如分布式文件系统，而Spark 提供了实时内存计算，速度非常快。有一点大家要注意，Spark并不是一定要依附于Hadoop才能生存，除了Hadoop的HDFS，还可以基于其他的云平台，当然啦，大家一致认为Spark与Hadoop配合默契最好摆了。

- b.技术趋势：Spark在崛起，hadoop和Storm中的一些组件在消退。大家在学习使用相关技术的时候，记得与时俱进掌握好新的趋势、新的替代技术，以保持自己的职业竞争力。

HSQL未来可能会被Spark SQL替代，现在很多企业都是HIVE SQL和Spark SQL两种工具共存，当Spark SQL逐步成熟的时候，就有可能替换HSQL；MapReduce也有可能被Spark 替换，趋势是这样，但目前Spark还不够成熟稳定，还有比较长的路要走；Hadoop中的算法库Mahout正被Spark中的算法库MLib所替代，为了不落后，大家注意去学习Mlib算法库；Storm会被Spark Streaming替换吗?在这里，Storm虽然不是hadoop生态中的一员，但我仍然想把它放在一起做过比较。由于Spark和hadoop天衣无缝的结合，Spark在逐步的走向成熟和稳定，其生态组件也在逐步的完善，是冉冉升起的新星，我相信Storm会逐步被挤压而走向衰退。

