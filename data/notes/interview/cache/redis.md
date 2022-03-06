# redis

* 面试题
  > zset 底层实现方式
  > redison热点key问题怎么解决
  > redis 雪崩
  > redis 跳表结构
  > redis RDB  AOF


* 基本数据结构

  > __string__
  ```shell
      SET + key + value
      GET + KEY
  ```  
  > __hash__  
  和java的hashmap  rehash不大一样，java是全部重新计算hash值，redis是渐进式hash，同步数据到新的hashtable，直到数据全部同步完毕
   ```shell
     HSET key valkey value
     HGET key valkey
     HGETAll key
  
     HSET key valkey intval
     HINREBY key valkey 1
  ```
  > __list__
   ```shell
  * 底层数据量小的时候是ziplist-连续的内存块,数据量大的时候将ziplist通过首尾指针首尾连接成双端队列
      RPUSH + key + value value value
      LPOP + key 
      LLEN + key
      LPUSH + key + value value value
      RPOP + key
      LRANGER + 0 -1
      LTRIM + start_index end_index
      LINDEX key + index
   ```
  > __set__
    ```shell
      等价于java的hashset,元素不重复
      SADD KEY  
      SMEMBERS KEY 查询某个set所有元素
      SISMEMBER KEY VAL  查询某个元素是否存在
      SPOP KEY   弹出一个元素
    ```
  > __zset__
    ```shell
      zset 内部是通过跳跃表实现的,
      ZSET 类似于java hashset和hashmap的综合,内存中的机构给每一个value配了一个权重值,这个权重值可以给元素排序做依据
      ZADD KEY SCORE VALUE
      ZRANGE KEY 0 -1    按权重值正序,输出
      ZRERANGE KEY 0 -1    按权重值倒序,输出
      ZCARD KEY     统计数量
      ZSCORE KEY val     获取指定值的score值
      ZRANK key val   获取指定值的排名
    ```
* 分布式锁
  > 死锁：释放问题-》过期时间  
  > 超时问题：业务时间过长，导致锁过期了，从而锁自动释放，这个时候可以使用线程Id或者随机数，但是这里有个问题，那即是需要先匹配key，
  > 然后再对比值，是一个费原子操作，这个时候需要使用原子操作脚本lua

* 消息队列
  > list 不可靠，会占用cpu ，解决方案：sleep但sleep时间不可靠，考虑使用阻塞队列 blpop  
  > 延时消息队列： zset  score设定为任务执行时间，以此作为延迟执行的时间，但是要考虑高可用，因此需要多线程轮询   












  