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



