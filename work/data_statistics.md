---
title: "data_statistics"
date: 2015-03-25 11:53
---
[TOC]
# 基础概念 #


##  数据分布 ##

伯努利分布 
    
    ○ where： 日常中的单次实验，且只有两种结果。如抛硬币。
    ○ 伯努利过程：就是重复多次的独立但是相同分布的伯努利实验组成，例如抛硬币十次。
    ○ 分布： 离散分布 0 1 

二项分布 [参考](http://zh.wikipedia.org/wiki/%E4%BA%8C%E9%A0%85%E5%88%86%E4%BD%88)
    
    n次的伯努利实验。
    

    一个简单的例子如下：掷一枚骰子十次，那么掷得4的次数就服从n = 10、p = 1/6的二项分布。
泊松分布[参考](http://zh.wikipedia.org/wiki/%E6%B3%8A%E6%9D%BE%E5%88%86%E4%BD%88)
    
    从二项分布推导出来的。

置信区间[参考](http://zh.wikipedia.org/wiki/%E7%BD%AE%E4%BF%A1%E5%8C%BA%E9%97%B4)

    概念 ： 在统计学中，一个概率样本的置信区间（Confidence interval）是对这个样本的某个总体参数的区间估计。置信区间展现的是这个参数的真实值有一定概率落在测量结果的周围的程度。置信区间给出的是被测量参数的测量值的可信程度，即前面所要求的“一定概率”。这个概率被称为置信水平。举例来说，如果在一次大选中某人的支持率为55%，而置信水平0.95上的置信区间是（50%,60%），那么他的真实支持率有百分之九十五的机率落在百分之五十和百分之六十之间，因此他的真实支持率不足一半的可能性小于百分之2.5（假设分布是对称的）。
    如例子中一样，置信水平一般用百分比表示，因此置信水平0.95上的置信区间也可以表达为：95%置信区间。置信区间的两端被称为置信极限。对一个给定情形的估计来说，置信水平越高，所对应的置信区间就会越大。
    对置信区间的计算通常要求对估计过程的假设（因此属于参数统计），比如说假设估计的误差是成正态分布的。
    置信区间只在频率统计中使用。在贝叶斯统计中的对应概念是可信区间。但是可信区间和置信区间是建立在不同的概念基础上的，因此一般上说取值不会一样。 置信空间表示通过计算估计值所在的区间。 置信水平表示准确值落在这个区间的概率。 置信区间表示具体值范围，置信水平是个概率值。例如：估计某件事件完成会在10~12日之间，但这个估计准确性大约只有80%：表示置信区间（10,12），置信水平80%。要想提高置信水平，就要放宽置信空间。

beta 分布。


bias 
    无偏什么恶的
    相当于期望

virance 
    过拟合什么的
    相当于方差

### 


##  评价指标 ##

Standardization Normalization
    
    在数据挖掘任务处理时，常常需要使用到数据的标准化（Standardization）和规范化（Normalization，归一化），前者使用数据范围变成[0,1]，后者则使数据均值=0，方差=1。原

    X_std = (X - X.min(axis=0)) / (X.max(axis=0) - X.min(axis=0))
    X_scaled = X_std * (max - min) + min


[auc](http://beader.me/2013/12/15/auc-roc/)
sklearn


关于log loss 

比赛采用的评价指标是LoglLoss：


至于离线评估为何更倾向采用logloss，而不是采用AUC值。Facebook在他们发布的论文【1】中提到现实环境中更加关注预测的准确性，而不是相对的排序。而AUC值更侧重相对排序，比如把整体的预测概率提升1倍，AUC值保持不变，但是logloss是有变化的。


# 特征 

##  特征hashing

特征hash 是一种降维方法。特征哈希法的目标是把原始的高维特征向量压缩成较低维特征向量，且尽量不损失原始特征的表达能力。

参考(http://blog.csdn.net/dm_ustc/article/details/45771757)

# 文章阅读 #

##  基于评分 ##

问题 ：  
    1. 同样评分，人多的8分，和人少的8分一样么？ 通过使用置信区间的下限来解决。
    2. 置信区间的下限，在n比较小的情况下，算的准确么？ 改进正太区间算法，使用威尔逊区间算法。
    3. 如果是top250，大众电影和小众电影怎么来分？ 引入先验概率。
    3. 评分的分布是正太么？ 5个评分权重是相等的么？ 引入秋里克雷分布。（先验分布+ 已有分布）

# 分类： 短文本解决思路 

[阅读](Large-Scale High-Precision Topic Modeling on Twitter)

基本思路:
    1. 用lda或者bigram 提取更多特征。

诡异思路:
    1. 有考虑用字来做特征的。


##  总结下广告点击预测 
基本概念
eCPM（effective cost per mille）指的就是每一千次展示可以获得的广告收入

离线计算

    合并数据

    特征笛卡尔积
    
    binarise / feature hashing
    训练
        正例全留
        打出bias图，然后调整模型
        打出feature曲线，然后调整模型。
        使用逻辑回归 来进行预测 。 需要优化梯度下降速度



在线广告系统ROI 

    -- investment
    -- return CTR * 点击价值  = eCPM



##  谷歌personal news recommendation based on

问题

    1. First, the system cannot recommend stories that have not yet been read by other users, a problem that is often referred to as the first-rater problem 
    2. 协同过滤没有考虑到人与人之间的不同性。
        Second, not all users are equal to each other, and the collaborative filtering method may not account for the individual variability between users [3]. For example, we observed that entertainment news stories are constantly recommended to most of the users, even for those users who never clicked on entertainment stories. The reason is that entertainment news stories are generally very popular, thus there are always enough clicks on entertainment stories from a user’s “neighbors” to make the recommendation.
##  最大熵模型

所以我们就想，能够弄出个模型，在符合已知知识的前提下，对未知事物不做任何假设，没有任何偏见。也就是让未知数据尽可能的自然。这就是最大熵模型(Maximum Entropy Models)了。
                            
# 在线广告系统

# 斯坦福机器学习公开课

model respresantation

cost function 

    常用: (h(x) - y)^2 minimize   -- square error function

# 推荐系统

##  content based systems

过程
    
    item representation: 为每个item抽取一些特征来表示这个item
    profile learning： 利用用户过去的action来学习出用户的洗好。
    recommendation generation： 通过比较上一步得到的用户的profile特征和item特征。为用户推荐一组相关性最大的item

基本思路
    
    一篇文章可以由向量来表示。
    profile 用向量来表示。
    计算两个向量的相似度。

### 怎么使用标签



## item_based cf and user-based cf 



## targeting 和 retargeting

重定向广告的含义是什么？它与定向广告有什么关系？

我的理解，重定向广告（retargeting）简单地说就是一种网页广告的定向技术，即针对广告受众（Audience）的某个属性，在同一个广告位，推送为他定制的广告到他的页面。重定向广告在我看来是定向广告的一种，而之所以有一个“重（Re-）”，是指的它的定向方式和其它定向广告有所不同。重定向广告是依据你之前的某个行为（Action，往往被记录在你的cookie中，也可能不是），把这个行为所触发的特定的广告，重新推送到你面前。这个行为往往是你访问了他的网页/或者店铺/搜索的了他的产品等。

一个重定向的scenario是：我在淘宝上搜索了手表，随便浏览了几个店铺A和店铺B，没有下定决心买。关了网页之后，cookie记录下了我的行为。之后去看了个个人博客，此人博客有加入广告联盟的广告位，我发现下面这个广告正好在推送淘宝上店铺C的手表，款式非常像我刚才爱淘宝搜索时点击的手表（比如我在淘宝搜索‘手表’，但最后点击/收藏的都是黑色皮带三针银表盘手表），我很感兴趣，点击了此广告，并且之后产生购买行为。


为什么会诞生这种技术？

因为可以带来更高的投资回报率。

在互联网广告的语境下，当人们谈论投资回报率的时候，通常都在谈论 Cost per 1000 Impressions,Click,Buy,Register,Actions..。相对于传统的门户广告，网盟广告，甚至传统的精准广告，重定向广告能够带来非常显著地Impression to click to buy的比率的提升。对于电商零售这种对conversion rate，返客率等比较敏感的广告主来说，重定向广告的优势会更明显。

scenario: 我在卖ebay一种针对新生婴儿的纯天然洗发水，我需要投放广告来倒流到我的ebay商品页。最早我的的投放策略是把我的广告放到yahoo的首页上去。然后我发现一天下来，yahoo花掉了我巨额的广告预算却只给我带来了非常少量的点击——1000个人看了只有1个人点击了我的广告。没错，大部分上yahoo首页的人都不会对一款婴儿洗发水感兴趣的。接下来我要考虑优化我的投放策略，于是我想到了Ad-Network：他们帮我把广告投放给了那些和他们有合作的母婴类网站上去，效果好多了，很显然上母婴网站的人们会对我的产品感兴趣，1000个人有10个人点击了我的广告。但是能不能做到更好呢？接下来一家做精准定向（targeting）广告的服务商找到了我，告诉我们他们能够直接把广告推送给那些刚刚生了北鼻的妈妈们，于是我选了这家vendor而他们给我的答卷是1000个新妈咪有100个对我的天然婴儿洗发水感兴趣（她们点击了，还有很多最后选择了购买）。好吧，作为一个挑剔的广告主我觉得这还不够，我说，能不能把我所有的媒介预算都花在刀刃上。这时候一家retargeting vendor出现了，他们说，交给我们把，你所有的广告都只会出现在那些刚刚试图找过你的新生婴儿纯天然洗发水的用户——我们不管他是一个人还是一条狗，但cookie显示那位用户确实在找类似的产品。那么对我来说，最后一个方案确实非常有吸引力

# user profile 

基本特征
    
    人口学: 性别，年龄、地域。etc
    内容特征: category, topic,keyword,entity,etc
        喜欢不喜欢
        短期、长期

    协同特征 : 用户
    其他: bige

例子:
    
    性别，年龄。
    顶级分类。
    兴趣分类来源。订阅来源。
    兴趣品牌，等等


算法

    点击加权 & 未点击惩罚
        iuf(类似idf) : 描述在用户群体里面的接受程度。

    热门点击 降权。
    时间衰减 : 比如婴儿的信息。


    不敢兴趣: 不感兴趣。
    噪声过滤 :spam, 标题党。



# 模型

##  gbdt

## lda
    
###     模型训练
    
步骤

    去掉数字
    去停用词
    去长度小于1，
    取n，v，a
    去标点


# 逻辑回归

## 与svm的区别

两种方法都是常见的分类算法，从目标函数来看，区别在于逻辑回归采用的是logistical loss，svm采用的是hinge loss。这两个损失函数的目的都是增加对分类影响较大的数据点的权重，减少与分类关系较小的数据点的权重。SVM的处理方法是只考虑support vectors，也就是和分类最相关的少数点，去学习分类器。而逻辑回归通过非线性映射，大大减小了离分类平面较远的点的权重，相对提升了与分类最相关的数据点的权重。两者的根本目的都是一样的。此外，根据需要，两个方法都可以增加不同的正则化项，如l1,l2等等。所以在很多实验中，两种算法的结果是很接近的。

但是逻辑回归相对来说模型更简单，好理解，实现起来，特别是大规模线性分类时比较方便。而SVM的理解和优化相对来说复杂一些。但是SVM的理论基础更加牢固，有一套结构化风险最小化的理论基础，虽然一般使用的人不太会去关注。还有很重要的一点，SVM转化为对偶问题后，分类只需要计算与少数几个支持向量的距离，这个在进行复杂核函数计算时优势很明显，能够大大简化模型和计算量。

##  过程




# 提升

`概念`
    每一步产生一个弱预测模型。并加权累加到总模型中。如果每一步的预测模型生成都是依据损失函数的梯度方向。则称之为
##  bagging
    
# svm

##  线性可分

##  线性支持向量机

##  非线性支持向量机


# ltr

##  https://bitbucket.org/tunystom/rankpy