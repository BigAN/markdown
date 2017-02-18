# scala



# 应该学些什么？

## 基本操作

scala的类型map，list 的基本操作。

list

> 	1. 如何构造slice  
> 	2. 如何

写文件操作

构建Map

```scala
val model_dict = Map(model_weights(0).zipWithIndex.map { case (k, v) => (v, k) }: _*)
```

### convert  any to float

```scala
z.asInstanceOf[Number].doubleValue
```

这句话的意思是 把any转为 number 实例 然后取 doubleValue 。 其他的也可以这么干，比如 string，然后toInt

##distinct count by key

## 日期

```scala
println((DateTime.now - 1.months).toString(DateTimeFormat .forPattern("yyyyMMdd"))) // returns org.joda.time.DateTime = 2009-06-27T13:25:59.195-07:00
```

## 偏函数

有两个接口isDefinedAt 和 apply

isDefinedAt 是指定偏函数的场景。

apply是 使用函数。

# spark

## spark 问题



### spark driver oom

- 解决task     过多导致的 driver oom, 通过coalesce对单个 stage的partition控制在1000以内。
- 解决saveastable     时因数据量过大导致的分区过多，造成driver  oom,     控制在5000以内的分区。
- 解决executor     oom， 因数据量较大，cores 设置较大的时候，executor 的并发度过高，每个core     的分得内存过小。



## spark 性能调优

### 基本

- executor memory

  > 缓存的数据大小，也是在需要 shuffle 操作的时候的如group,等的操作。

- num executors

- 注意

  > --executor-memory/spark.executor.memory 控制 *executor* 的堆的大小，但是 JVM 本身也会占用一定的堆空间，比如内部的 String 或者直接 byte buffer，*executor* memory 的 spark.yarn.executor.memoryOverhead 属性决定向 **YARN** 请求的每个 *executor* 的内存大小，默认值为max(384, 0.7 * spark.executor.memory);

  > 在运行微型 *executor* 时（比如只有一个core而且只有够执行一个task的内存）扔掉在一个JVM上同时运行多个task的好处。比如 broadcast 变量需要为每个 *executor* 复制一遍，这么多小executor会导致更多的数据拷贝。

- 例子

  > 6个节点有NodeManager在上面运行，每个节点有16个core以及64GB的内存
  >
  > 基本配置 
  >
  > --num-executors 6 --executor-cores 15 --executor-memory 63G。 (留我们避免使用 100% 的 **YARN** container 资源因为还要为 OS 和 hadoop 的 Daemon 留一部分资源。在上面的场景中，我们预留了1个core和1G的内存给这些进程)

  > 所以看起来我们最先想到的配置会是这样的：--num-executors 6 --executor-cores 15 --executor-memory 63G。但是这个配置可能无法达到我们的需求，因为： 
  >
  > - 63GB+ 的 *executor* memory 塞不进只有 63GB 容量的 NodeManager； 
  >
  > - 应用的 master 也需要占用一个core，意味着在某个节点上，没有15个core给 *executor* 使用； 
  >
  > - 15个core会影响 HDFS IO的吞吐量。 
  >   配置成 --num-executors 17 --executor-cores 5 --executor-memory 19G 可能会效果更好，因为： 
  >
  > - 这个配置会在每个节点上生成3个 *executor*，除了应用的master运行的机器，这台机器上只会运行
  >
  >   2个 *executor* 
  >
  > - --executor-memory 被分成3份（63G/每个节点3个executor）=21。 21 * （1 - 0.07） ~ 19。

  ​

- task 数量。

  > task 数量 与stage 的上个一个rdd 的partition 数量相同。
  >
  >  过少的 *task* 个数可能会导致在一些聚集操作时， 每个 *task* 的内存压力会很大。任何 **join**，**cogroup**，***ByKey** 操作都会在内存生成一个 hash-map或者 buffer 用于分组或者排序。**join**， **cogroup** ，**groupByKey** 会在
  >
  >  *shuffle* 时在 fetching 端使用这些数据结构， **reduceByKey** ，**aggregateByKey** 会在 *shuffle* 时在两端都会使用这些数据结构。
  >
  > 当需要进行这个聚集操作的 *record* 不能完全轻易塞进内存中时，一些问题会暴露出来。首先，在内存 hold 大量这些数据结构的 *record* 会增加 GC的压力，可能会导致流程停顿下来。其次，如果数据不能完全载入内存，Spark 会将这些数据写到磁盘，这会引起磁盘 IO和排序。在 Cloudera 的用户中，这可能是导致 Spark Job 慢的首要原因。

- storage memoryfraction

  - rdd 持久化的数据能使用多少内存所占的比例。
  - 适当提高，保证数据能更多的缓存数据

- storage memoryfraction

  - shuffle 操作所占的内存比例。若超出内存限制，则会写入 到磁盘，造成速度减慢。
  - ​



### 数据倾斜

#### 的