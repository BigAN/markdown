typora-copy-images-to: ../markdown

# spark							

```
--conf spark.shuffle.blocksize.threshold=32
上面的参数意思是当某一个block 超过32M会写到磁盘
shuffle read 时候，block过大就不会导致堆外OOM
```

driver oom : 

1. 分区数量过多。导致driver 中收到的日志过多。 — coalcose
2. collect 等操作。
3. ​

# others





似乎 frame_size 的大小描述的是程序的大小，而不是程序结果的大小。

## 一.org.apache.spark.shuffle.FetchFailedException

### 1.问题描述

这种问题一般发生在有大量shuffle操作的时候,task不断的failed,然后又重执行，一直循环下去，非常的耗时。

![faild](http://doc.ithao123.cn/d/fb/ec/be/fbecbe95205fc0b89605a1ec2119bb12.jpg)

### 2.报错提示

**(1) missing output location**

```
org.apache.spark.shuffle.MetadataFetchFailedException: Missing an output location for shuffle 0
```

![missing output location](http://doc.ithao123.cn/d/92/a3/ce/92a3ce7dda16d33f8cb1927f7b0482f1.jpg)

**(2) shuffle fetch faild**

```
org.apache.spark.shuffle.FetchFailedException: Failed to connect to spark047215/192.168.47.215:50268
```

![shuffle fetch faild](http://doc.ithao123.cn/d/5a/ea/fb/5aeafb3c1757f2c2154634b424fb6353.jpg)

当前的配置为每个executor使用1cpu,5GRAM,启动了20个executor

### 3.解决方案

一般遇到这种问题提高executor内存即可,同时增加每个executor的cpu,这样不会减少task并行度。

- spark.executor.memory 15G
- spark.executor.cores 3
- spark.cores.max 21

启动的execuote数量为:7个

```
execuoteNum = spark.cores.max/spark.executor.cores 

```

每个executor的配置：

```
3core,15G RAM

```

消耗的内存资源为:105G RAM

```
15G*7=105G

```

可以发现使用的资源并没有提升，但是同样的任务原来的配置跑几个小时还在卡着，改了配置后几分钟就结束了。

## 二.Executor&Task Lost

### 1.问题描述

因为网络或者gc的原因,worker或executor没有接收到executor或task的心跳反馈

### 2.报错提示

**(1) executor lost**

```
WARN TaskSetManager: Lost task 1.0 in stage 0.0 (TID 1, aa.local): ExecutorLostFailure (executor lost)
```

**(2) task lost**

```
WARN TaskSetManager: Lost task 69.2 in stage 7.0 (TID 1145, 192.168.47.217): java.io.IOException: Connection from /192.168.47.217:55483 closed
```

**(3) 各种timeout**

```
java.util.concurrent.TimeoutException: Futures timed out after [120 second
```

```
ERROR TransportChannelHandler: Connection to /192.168.47.212:35409 has been quiet for 120000 ms while there are outstanding requests. Assuming connection is dead; please adjust spark.network.timeout if this is wrong
```

### 3.解决方案

提高 **spark.network.timeout** 的值，根据情况改成300(5min)或更高。

默认为 120(120s),配置所有网络传输的延时，如果没有主动设置以下参数，默认覆盖其属性

- spark.core.connection.ack.wait.timeout
- spark.akka.timeout
- spark.storage.blockManagerSlaveTimeoutMs
- [spark.shuffle.io](http://spark.shuffle.io/).connectionTimeout
- spark.rpc.askTimeout or spark.rpc.lookupTimeout

## 三.倾斜

### 1.问题描述

大多数任务都完成了，还有那么一两个任务怎么都跑不完或者跑的很慢。 
分为数据倾斜和task倾斜两种。

### 2.错误提示

**(1) 数据倾斜**

![数据倾斜](http://doc.ithao123.cn/d/8d/75/91/8d75911adc56d8be935f5bf8d3f2eb73.jpg)

**(2) 任务倾斜**

差距不大的几个task,有的运行速度特别慢。

### 3.解决方案

**(1) 数据倾斜**

数据倾斜大多数情况是由于大量`null`值或者`""`引起，在计算前过滤掉这些数据既可。 
例如：

```
sqlContext.sql("...where col is not null and col != ''")

```

**(2) 任务倾斜**

task倾斜原因比较多，网络io,cpu,mem都有可能造成这个节点上的任务执行缓慢，可以去看该节点的性能监控来分析原因。以前遇到过同事在spark的一台worker上跑R的任务导致该节点spark task运行缓慢。 
或者可以开启spark的推测机制，开启推测机制后如果某一台机器的几个task特别慢，推测机制会将任务分配到其他机器执行，最后Spark会选取最快的作为最终结果。

- spark.speculation true
- spark.speculation.interval 100 - 检测周期，单位毫秒；
- spark.speculation.quantile 0.75 - 完成task的百分比时启动推测
- spark.speculation.multiplier 1.5 - 比其他的慢多少倍时启动推测。

## 四.OOM（内存溢出）

### 1.问题描述

内存不够，数据太多就会抛出OOM的Exeception

因为报错提示很明显，这里就不给报错提示了。。。

### 2.解决方案

主要有driver OOM和executor OOM两种

**(1) driver OOM**

一般是使用了collect操作将所有executor的数据聚合到driver导致。尽量不要使用collect操作即可。

**(2) executor OOM**

1.可以按下面的内存优化的方法增加code使用内存空间

2.增加executor内存总量,也就是说增加spark.executor.memory的值

3.增加任务并行度（大任务就被分成小任务了)，参考下面优化并行度的方法

## 优化

### 1.内存

当然如果你的任务shuffle量特别大，同时rdd缓存比较少可以更改下面的参数进一步提高任务运行速度。

`spark.storage.memoryFraction` － 分配给rdd缓存的比例，默认为0.6(60%)，如果缓存的数据较少可以降低该值。

`spark.shuffle.memoryFraction` - 分配给shuffle数据的内存比例，默认为0.2(20%)

剩下的20%内存空间则是分配给代码生成对象等。

如果任务运行缓慢，jvm进行频繁gc或者内存空间不足，或者可以降低上述的两个值。

`"spark.rdd.compress","true"` － 默认为false，压缩序列化的RDD分区,消耗一些cpu减少空间的使用

如果数据只使用一次，不要采用cache操作，因为并不会提高运行速度，还会造成内存浪费。

### 2.并行度

`spark.default.parallelism`

发生shuffle时的并行度，在standalone模式下的数量默认为core的个数，也可手动调整，数量设置太大会造成很多小任务，增加启动任务的开销，太小，运行大数据量的任务时速度缓慢。

`spark.sql.shuffle.partitions`

sql聚合操作(发生shuffle)时的并行度，默认为200,如果任务运行缓慢增加这个值。

相同的两个任务： 
spark.sql.shuffle.partitions=300:

![并行度300](http://doc.ithao123.cn/d/bb/37/58/bb375894ef733c83e1d3818d2d469ff8.jpg)

spark.sql.shuffle.partitions=500:

![并行度500](http://doc.ithao123.cn/d/13/d8/fd/13d8fd74164f17a1acbcc793eab2ebae.jpg)

速度变快主要是大量的减少了gc的时间。

修改map阶段并行度主要是在代码中使用`rdd.repartition(partitionNum)`来操作。

[Like](http://wiki.sankuai.com/pages/viewpage.action?pageId=375505606)Be the first to like th



# 资源配置

**一、动态资源分配**

**1、yarn配置**

\##修改
<property>
<name>yarn.nodemanager.aux-services</name>
<value>mapreduce_shuffle,**spark_shuffle**</value>
</property>
\##增加
<property>
<name>yarn.nodemanager.aux-services.spark_shuffle.class</name>
<value>org.apache.spark.network.yarn.YarnShuffleService</value>
</property>
<property>
<name>spark.shuffle.service.port</name>
<value>7337</value>
</property>

将$SPARK_HOME/lib/spark-1.4.1-yarn-shuffle.jar拷贝到每台NodeManager的${HADOOP_HOME}/share/hadoop/yarn/lib/下。

重启所有NodeManager。

**2、spark配置**

--master yarn-client \
-c spark.driver.memory=36g \
-c spark.shuffle.service.enabled=true \
-c spark.shuffle.service.port=7337 \
-c spark.dynamicAllocation.enabled=true \
-c spark.dynamicAllocation.minExecutors=100 \
-c spark.dynamicAllocation.maxExecutors=200 \
-c spark.dynamicAllocation.initialExecutors=100 \
-c spark.dynamicAllocation.schedulerBacklogTimeout=1s

**说明：**

目前，由于线上yarn配置更改比较困难，同时考虑到配置动态资源分配后，数据本地化可能会出现问题，因此暂时选用固定资源分配。

**二、固定资源分配**

| **任务可用总资源：**memory：3750000mbcores：1500 | **任务建议分配资源：**memory：1250000mcores: 600~800 |
| -------------------------------------- | ---------------------------------------- |
|                                        |                                          |

| **Job_id**                | **start_time**      | **end_time**        | **time taken** | **方案** |
| ------------------------- | ------------------- | ------------------- | -------------- | ------ |
| **1476359393858_1979770** | 2016/10/24 10:45:31 | 2016/10/24 13:21:28 | 2:35:57        | 原始方案   |
| **1476359393858_1853609** | 2016/10/25 16:17:43 | 2016/10/25 18:45:03 | 2:27:20        | 原始方案   |
| **xxxxxxxxxxxx_xxxxxxx**  | xxxxxxxxxx xxxxxxx  | xxxxxxxxxx xxxxxxx  | error          | 方案1    |
| **1476359393858_2025449** | 2016/10/26 17:17:54 | 2016/10/26 19:40:10 | 2:22:16        | 方案2    |
| **1476359393858_2058222** | 2016/10/26 20:32:43 | 2016/10/26 22:46:13 | 2:13:30        | 方案2    |
| **1476359393858_2179115** | 2016/10/27 11:55:26 | 2016/10/27 15:32:01 | 3:36:35        | 方案3    |
| **1476359393858_2247468** | 2016/10/27 20:55:35 | 2016/10/27 22:57:57 | 2:2:22         | 方案4    |
| **1476359393858_2363067** | 2016/10/28 12:02:25 | 2016/10/28 16:12:34 | 4:10:09        | 方案4    |
| **1476359393858_2397635** | 2016/10/28 18:00:49 | 2016/10/28 20:46:55 | 2:46:06        | 方案5    |
| **1476359393858_2882512** | 2016/10/31 20:31:15 | 2016/10/31 23:19:29 | 2:48:14        | 方案6    |
| **1476359393858_3170421** | 2016/11/02 11:50:28 | 2016/11/02 15:46:38 | 3:56:10        | 方案6    |
| **1476359393858_3220102** | 2016/11/02 18:16:38 | 2016/11/02 21:31:42 | 3:15:04        | 方案7    |
| **1476359393858_3347590** | 2016/11/03 11:20:41 | 2016/11/03 13:12:17 | 1:51:36        | 方案8    |
| **1476359393858_3350665** | 2016/11/03 11:47:11 | 2016/11/03 13:59:13 | 2:12:02        | 方案8    |
| **1476359393858_3373502** | 2016/11/03 15:47:59 | 2016/11/03 19:34:28 | 3:46:29        | 方案8    |

| 原始方案                                     | **方案一**                                  | **方案二**                                  |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| --num-executors 200--executor-cores 6--executor-memory 7g--driver-memory 48g | --num-executors 100--executor-cores 8--executor-memory 12g--driver-memory 4g-c spark.default.parallelism=1600 | --num-executors 200--executor-cores 4--executor-memory 6g--driver-memory 4g-c spark.default.parallelism=1600---------------------------------------------c spark.speculation=true |

| **方案三**                                  | **方案四**                                  | **方案五**                                  |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| --num-executors 300--executor-cores 2--executor-memory 2g--driver-memory 4g-c spark.default.parallelism=1600-c spark.speculation=true-c spark.speculation.multiplier=2 | --num-executors 300--executor-cores 2--executor-memory 4g--driver-memory 4g-c spark.default.parallelism=1200-c spark.speculation=true | --num-executors 300--executor-cores 2--executor-memory 3g--driver-memory 4g-c spark.default.parallelism=1200-c spark.speculation=true |

| **方案六**                                  | **方案七**                                  | **方案八**                                  |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| num-executors:200executor-cores:1executor-memory:1gdriver-memory:1g-c spark.default.parallelism 400-c spark.speculation=true | num-executors:100executor-cores:2executor-memory:2gdriver-memory:1g-c spark.default.parallelism 400-c spark.speculation=true-c spark.shuffle.consolidateFiles=true | num-executors:100executor-cores:2executor-memory:2gdriver-memory:1g-c spark.default.parallelism 400-c spark.speculation=true-c spark.shuffle.consolidateFiles=true-c spark.serializer=org.apache.spark.serializer.KryoSerializer |

| **方案九**                                  | **方案十**                                  | **方案十一**                                 |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| num-executors:100executor-cores:2executor-memory:2gdriver-memory:1g-c spark.default.parallelism 400-c spark.speculation=true-c spark.shuffle.consolidateFiles=true-c spark.serializer=org.apache.spark.serializer.KryoSerializer -c spark.scheduler.mode=Fair | num-executors:100executor-cores:2executor-memory:2gdriver-memory:1g-c spark.default.parallelism 400-c spark.speculation=true-c spark.speculation.quantile=0.85-c spark.shuffle.consolidateFiles=true-c spark.serializer=org.apache.spark.serializer.KryoSerializer -c spark.scheduler.mode=Fair-c spark.locality.wait = 1000 | num-executors:100executor-cores:2executor-memory:2gdriver-memory:1g-c spark.default.parallelism 400-c spark.speculation=true-c spark.speculation.quantile=0.85-c spark.shuffle.consolidateFiles=true-c spark.serializer=org.apache.spark.serializer.KryoSerializer -c spark.scheduler.mode=Fair-c spark.yarn.submit.file.replication=6-c spark.locality.wait = 1000 |

****

**说明：**
按照原始方案，总共申请的CPU核数是200*6=1200个，但是每个stage运行的task数最大是500，正常情况下，同一时间每个核运行一个task，也就是说有700个核是空闲的。集群这边总共给midas_online这个账号分配的内存资源memory:3750000mb，现在一个任务占用内存是200*7＋48=1448g，也就是1482752mb，同时跑两个任务基本上占用了账号80%的内存资源，另外集群给账号分配了cpu核数vCores:1500，但是现在一个任务就占用了1200，有点多。

stage 1：

1、初步想法是减少任务使用的cpu核数，增大并行的task数量，同时适当减少每个task占用的内存（因为我发现，任务执行时每个task的数据量最大也就256m左右），基本保证使用的总资源不超过账号分配资源的1/3～1/2，保证这个任务运行的同时尽量不影响其它任务的运行，按照这个的原则，初步定了方案一和方案二（由于yarn配置里面限制了调度时一个container能够申请的最大资源为8g，方案一失败）。

2、然后发现任务耗时主要集中在从磁盘读写数据的stage上，而且一个stage中不同task的执行速度倾斜比较严重，最快的几秒、十几秒就可以执行完，慢的需要几分钟，整体执行速度被这些任务拖慢了。因此开启了spark的推测机制，推测机制会定时检测任务的执行进度，将执行慢的任务放到其它机器上重新跑，和原来任务对比，选择其中最先完成的（据此制定了方案二的改进版）。实际测试显示任务执行总耗时为2小时13分钟，相比于之前正常运行时的两个半小时，略有提升，占用的总资源已经差不多减到原来的2/3。

3、为了进一步提高任务的执行速度，降低资源占用，增加了executors数，降低了核数和内存，将总资源降到了原来的一半（见方案三），但这次任务的执行速度要比之前明显慢很多，怀疑可能的原因：一是内存分配太少，二是executor分配太多，据此修正得到了方案四，首次测试任务的执行速度缩短到了2小时2分钟，但是再次测试时又需要四个多小时。

4、通过之前的测试意识到，任务的执行速度受集群当前的资源状况影响很大，于是分不同的时段测试了方案五，发现因为现在的配置大大降低了任务申请的总资源，在集群资源充裕的时候，申请的资源都能够拿到，任务运行是没有问题的，而且可能比原来更快，但是在资源紧张的情况下，任务申请的全部资源只能拿到一部分，那么假设比例相同的情况下，申请的总资源越多，能拿到的部分就越多，所以任务运行速度会有明显的差别。

stage 2：

5、了解到早晨9点之前，集群ad账号可用资源一共只有589个core，决定进一步大幅度降低spark任务申请资源的总量，得到方案六。此时spark任务申请的cpu核数仅有最初方案的1/6，内存仅有最初的1/7，但是任务执行时间明显变慢。

6、方案七调整了executor个数，以求在资源总量不变的情况下，更合理的分配申请到的资源。同时设置spark.shuffle.consolidateFiles项为true，合并shuffle write的输出文件，减少磁盘IO开销。测试结果显示，该方案任务运行速度并无明显提升。

7、方案八设置spark序列化对象使用的类为org.apache.spark.serializer.KryoSerializer，而非默认类org.apache.spark.serializer.JavaSerializer。测试发现任务执行速度有明显提升，但是由于测试环境不同，影响因素复杂，不能确定是否是该参数造成的。于是对方案八进行了多次测试，发现任务执行速度相差较大，对于耗时较长的任务进行分析发现，大部分时间消耗在了等待调度上，因此更改spark任务的调度方案为Fair，得到了方案九。

 8、再次研究了spark所有可以配置的参数，列出了其余可能影响任务执行速度的参数，并根据官方给出的参数设置建议，对相关参数进行调整，形成了方案十和方案十一，但是由于近两天集群运行速度较慢，测试结果不具备参考价值，所以具体情况还有待观察。

