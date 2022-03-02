# HDFS

* 介绍

  > HDFS 是一个分布式文件系统，就像任何其它文件系统，它允许用户使用shell 命令操作文件系统。 Hadoop支持很多Shell命令，可以查看HDFS文件系统的目录结构、上传和下载数据、创建文件等。
  > 实际上有三种shell命令方式，分别是：  
  > __hadoop fs__：适用于多种不同的文件系统，比如本地文件系统和HDFS文件系统。  
  > __hadoop dfs__：只能适用于HDFS文件系统（已弃用）。  
  > __hdfs dfs__：跟hadoop dfs的命令作用一样，也只能适用于HDFS文件系统。


* HDFS文件操作常用命令

  > hadoop fs -ls <path>：显示 <path>指定的文件的详细信息。  
  > hadoop fs ls -R <path>：ls命令的递归版本。   
  > hadoop fs -cat <path>：将<path>指定的文件的内容输出到标准输出。   
  > hadoop fs -chgrp [-R] group <path>：将<path>指定的文件所属的组改为group，使用-R对<path>指定的文件夹内的文件进行递归操作。这个命令只适用于超级用户。   
  > hadoop fs -chown [-R] [owner] [:[group]] <path>：改变<path>指定的文件的拥有者，-R用于递归改变文件夹内的文件的拥有者。这个命令只适用于超级用户。   
  > hadoop fs -chmod [-R] <mode> <path>：将<path>指定的文件的权限更改为<mode>。这个命令只适用于超级用户和文件的所有者。   
  > hadoop fs -tail [-f] <path>：将<path>指定的文件最后1KB的内容输出到标准输出上。-f选项用于持续检测新添加到文件中的内容。   
  > hadoop fs -stat [format] <path>：以指定的格式返回<path>指定的文件的相关信息。当不指定format的时候，返回文件<path>的创建日期。[format]可选参数有：%b（文件大小）、%o（Block 大小）、%n（文件名）、%r（副本个数），%y（最后一次修改日期和时间）。   
  > hadoop fs -touchz <path>：创建一个<path>指定的空文件。   
  > hadoop fs -mkdir [-p] <paths>：创建<paths>指定的一个或多个文件夹，-p选项用于递归创建子文件夹。   
  > hadoop fs -copyFromLocal <localsrc> <dst>：将本地源文件<localsrc>复制到路径<dst>指定的文件或文件夹中。   
  > hadoop fs -copyToLocal [-ignorecrc] [-crc] <target> <localdst>：将目标文件<target>复制到本地文件或文件夹<localdst>中，可用-ignorecrc选项复制CRC校验失败的文件，使用-crc选项复制文件以及CRC信息。   
  > hadoop fs -cp ：将文件从源路径<src>复制到目标路径<dst>。   
  > hadoop fs -du <path>：显示<path>指定的文件或文件夹中所有文件的大小。   
  > hadoop fs -du -s <path>：显示<path>路径下所有文件和的大小。   
  > hadoop fs -du - h <path>：显示<path>路径下每个文件夹和文件的大小，文件的大小用方便阅读的形式表示，例如用64M代替67108864。   
  > hadoop fs -expunge：清空回收站。   
  > hadoop fs -get [ignorecrc] [-crc] <src> <localdst>：复制<src>指定的文件到本地文件系统<localdst>指定的文件或文件夹，可用-ignorecrc选项复制CRC校验失败的文件，使用-crc选项复制文件以及CRC信息。   
  > hadoop fs -getmerge [-nl] <src> <localdst>：对<src>指定的源目录中的所有文件进行合并，写入<localdst>指定的本地文件。-nl是可选的，用于指定在每个文件结尾添加一个换行符。   
  > hadoop fs -put <localsrc> <dst>：从本地文件系统中复制<localsrc>指定的单个或多个源文件到<dst>指定的目标文件系统中，也支持从标准输入中读取输入写入目标文件系统。   
  > hadoop fs -moveFromLocal <localsrc> <dst>：与put命令相同，但是文件上传结束后会从本地文件系统中删除<localsrc>指定的文件。   
  > hadoop fs -mv <src> <dst>：将文件从源路径<src>移动到目标路径<dst>。   
  > hadoop fs -rm <path>：删除<path>指定的文件，只删除非空目录和文件。   
  > hadoop fs -rm -r <path>：删除<path>指定的文件夹及其下的所有文件，-r选项表示递归删除子目录。   
  > hadoop fs -setrep [-R] <path>：改变<path>指定的文件的副本系数，-R选项用于递归改变目录下所有文件的副本系数。   
  > hadoop fs -text <path>：将<path>指定的文本文件或某些格式的非文本文件通过文本格式输出，文件的格式允许是zip和TextRecordInputStream等。   
  > hadoop fs -count <path>：统计<path>路径下的目录个数、文件个数、文件总计大小。显示为目录个数、文件个数、文件总计大小、输入路径。   
  > hadoop fs -test -[ezd] <path>：检查<path>指定的文件或文件夹的相关信息。不同选项的作用如下：   
  > -e：检查文件是否存在，如果存在则返回0，否则返回1。   
  > -z：检查文件是否是0字节，如果是则返回0，否则返回1。   
  > -d：如果路径是个目录，则返回1，否则返回0。   

  
*











