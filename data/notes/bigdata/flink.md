# FLINK

* 数据集类型

  > 无穷数据集：无穷的持续集成的数据集合 如：业务的实时数据  
  > 有界数据集：有限不会改变的数据集合 如：业务的历史数据

* 数据运算模型

  > 流式：只要数据一直在产生，计算就持续地进行  
  > 批处理：在预先定义的时间内运行计算，当完成时释放计算机资源

* Flink 整体结构
  > 1、部署：Flink 支持本地运行、能在独立集群或者在被 YARN 或 Mesos 管理的集群上运行， 也能部署在云上。  
  > 2、运行：Flink 的核心是分布式流式数据引擎，意味着数据以一次一个事件的形式被处理。  
  > 3、API：DataStream、DataSet、Table、SQL API。  
  > 4、扩展库：Flink 还包括用于复杂事件处理，机器学习，图形处理和 Apache Storm 兼容性的专用代码库。

* 程序与数据流结构

> 1、Source: 数据源，Flink 在流处理和批处理上的 source 大概有 4 类：
> > __基于本地集合的 source、__
> > __基于文件的 source、__
> > __基于网络套接字的 source、__
> > __自定义的 source__ : Apache kafka、Amazon Kinesis Streams、RabbitMQ、Twitter Streaming API、Apache NiFi 等，当然你也可以定义自己的 source。  
> 2、Transformation：数据转换的各种操作，有 __Map / FlatMap / Filter / KeyBy / Reduce / Fold / Aggregations / Window / WindowAll / Union / Window join / Split / Select / Project__ 等  
> 3、Sink：接收器，Flink 将转换计算后的数据发送的地点 ，你可能需要存储下来，Flink 常见的 Sink 大概有如下几类：写入文件、打印出来、写入 socket 、自定义的 sink 。自定义的 sink 常见的有 Apache kafka、RabbitMQ、MySQL、ElasticSearch、Apache Cassandra、Hadoop FileSystem 等，同理你也可以定义自己的 sink。