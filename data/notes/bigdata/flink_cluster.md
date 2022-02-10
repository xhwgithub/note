# BUILD ENVIRONMENT

前言
> flink集群可以跑在很多环境上面，包括yarn、standalone、mesos等等很多平台，本文章就先从standalone搭建开始。先说一下我的环境
> 我是centos7，并且已经安装了jdk1.8版本，Scala2.11版本，读者如果想要跟随我安装这个版本的，请自行安装好这些。

https://www-eu.apache.org/dist/flink/flink-1.9.1/flink-1.9.1-bin-scala_2.11.tgz

* 解压
  > tar -zxvf flink-1.9.1-bin-scala_2.11.tgz -C /opt/bigdata/ 上面的命令可以指定解压的目录，可以根据自己服务器的实际情况来指定。

* 修改名字
  > cp flink-1.9.1-bin-scala_2.11 mv flink-1.9.1-bin-scala_2.11 flink 修改配置文件 vim conf/flink-conf.yaml

  > jobmanager.rpc.address: node1 # 这里定于rpc地址，可以认为是master地址    
  > jobmanager.heap.size: 1024M # 这里是jvm多少给jobmanager分配，根据自己的大小来配置   
  > taskmanager.heap.size：1024 # taskManager的内存大小，根据自己的来配置    
  > parallelism.default：1 # cpu分配多少，根据自己实际情况来定    
  > io.tmp.dirs: /tmp #指定临时目录，最好自己创建一个 然后再修改

* vim conf/slaves

  > 139.198.116.78:8080  
  > 139.198.116.79:8080   
  > 通过配置文件来解释一下，首先rpc的地址指定的是主master地址，slaves指定的是从节点的地址，我这里node1是主节点，node2和node3是从节点。

配置环境变量 将flink的目录配置到环境变量中

* vim ~/.bash_profile

  > FLINK_HOME=/opt/bigdata/flink
  > PATH=$FLINK_HOME/bin
  > export FLINK_HOME

source ~/.bash_profile 发送文件 将之前的flink文件发往其他的节点

scp -r flink node2:$PWD scp -r flink node3:$PWD 将bash_profile文件也发送过去

scp -r ～/.bash_profile node2:$PWD scp -r ～/.bash_profile node3:$PWD 在node2和node3上面记得也要source一下哈。

启动集群 start-cluster.sh 这个时候你会看到如下打印输出，记得上面的操作要做主节点执行哈，比如我在node1上面执行。  
然后我用jps会在node1上看到 在node2和node3上面都是看到 那恭喜你，到现在已经搭建集群完毕！