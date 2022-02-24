# flink 调研

* 输入输出数据源支持

  > Local File System    
  > MongoDB    
  > HBase    
  > Apache Flume  
  > MQ kafka rabbitmq  
  > Apache Kafka (source/sink)  
  > Apache Cassandra (sink)  
  > Amazon Kinesis Streams (source/sink)  
  > Elasticsearch (sink)  
  > FileSystem (Hadoop Distributed File System)  
  > RabbitMQ (source/sink)  
  > Google PubSub (source/sink)  
  > Hybrid Source (source)  
  > Apache NiFi (source/sink)  
  > Apache Pulsar (source)  
  > Twitter Streaming API (source)  
  > JDBC (MySQL, Oracle, MS SQL etc.)  
  > REST (HTTP TCP SOCKET)

* 监控

  > FLINK 自带web监控界面

* 扩容 Flink： 1.添加机器是，必须修改内容：

  > https://blog.csdn.net/qq_42021375/article/details/103513766

* 支持的语言

  > SCALA、PYTHON、JAVA、SQL

* 批处理 流处理

  > StreamExecutionEnvironment.getExecutionEnvironment();  
  > 本身支持历史数据批处理，强项是实时数据的流处理

* 实时数据性能

  > 所有实时处理引擎中性能最好的（spark-streaming 实时处理其实是微批量处理，数据延迟没有flink好）

* 机器学习

  > FLINK-ML

* SQL 拓展
  > 自定义函数，直接低啊用

* 方案
  > 实时处理数据流向逻辑 ，不写业务逻辑（sql转换拉取数据）
