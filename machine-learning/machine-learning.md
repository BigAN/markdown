---
title: "machine-learning"
date: 2015-04-13 14:18
---

# 基本概念 #

# 置信度 #
就是条件概率。 关联规则有用到。
# 推荐系统 #
## 推荐系统文章 ##
单纯从上，书建议 
项亮 著的《推荐系统实践》 
蒋帆 译的《推荐系统》。
论文方面，有科学网上一些人组织的顺序：
1. 中文综述(了解概念-入门篇)
a) 个性化推荐系统的研究进展 ok
b) 个性化推荐系统评价方法综述 ok
2. 英文综述(了解概念-进阶篇)
a) 2004ACMTois-Evaluating collaborative filtering recommender systems ok
b) 2004ACMTois -Introduction to Recommender Systems - Algorithms and evaluation
c) 2005IEEEtkde Toward the next generation of recommender systems - A survey of the state-of-the-art and possible extensions ok
3. 动手能力(实践算法-入门篇)
a) 2004ACMtois Item-based top-N recommendation algorithms(协同过滤) ok
b) 2007PRE Bipartite network projection and personal recommendation(网络结构) ok
4. 动手能力(实践算法-进阶篇)
a) 2010PNAS-Solving the apparent diversity-accuracy dilemma of recommender systems (物质扩散和热传导) ok
b) 2009NJP Accurate and diverse recommendations via eliminating redundant correlations (多步物质扩散) ok
c) 2008EPL Effect of initial configuration on network-based Recommendation (初始资源分配问题) NO
5. 推荐系统扩展应用(进阶篇)
a) 2009EPJB Predicting missing links via local information(相似性度量方法)
b) 2010theis-Evaluating Collaborative Filtering over time(基于时间效应的博士论文)
c) 2009PA Personalized recommendation via integrated diffusion on user-item-tag tripartite graphs (基于标签的三部分图方法) ok
d) 2004LNCS Trust-aware collaborative filtering for recommender systems（基于信任机制） ok
e) 1997CA-Fab_content-based, collaborative recommendation(基于文本信息)
6. 推荐结果的解释(进阶篇)
a) 2000CSCW-Explaining Collaborative Filtering Recommendations ok
b) 2011PRE-Information filtering via biased heat conduction
c) 2011PRE- Information filtering via preferential diffusion ok
d) 2010EPL Link Prediction in weighted networks - The role of weak ties ok
e) 2010EPL-Solving the cold-start problem in recommender systems with social tags ok
7. 推荐系统综合篇(专著、大型综述、博士论文)
a) 2005Ziegler-thesis-Towards Decentralized Recommender Systems ok
b) 2010Recommender Systems Handbook


# 工具 #
## jieba ##
打印词性

    tmp = json.dumps([(x.word,x.flag) for x in words],encoding="utf-8",ensure_ascii=False)

(词性标注表)[]
    
    名词
    nr 人名
        nr1 汉语姓氏
        nr2 汉语名字
        nrj 日语人名
        nrf 音译人名
    ns 地名
    　nsf 音译地名
    nt 机构团体名
    nz 其它专名
    nl 名词性惯用语
    ng 名词性语素

    t 时间词
    　　tg 时间词性语素

    s 处所词

    f 方位词

    v 动词
        vd 副动词
        vn 名动词
        vshi 动词“是”
        vyou 动词“有”
        vf 趋向动词
        vx 形式动词
        vi 不及物动词（内动词）
        vl 动词性惯用语
        vg 动词性语素
    a 形容词
        ad 副形词
        an 名形词
        ag 形容词性语素
        al 形容词性惯用语
    b 区别词
        bl 区别词性惯用语
    z 状态词
    r 代词
        rr 人称代词
        rz 指示代词
            rzt 时间指示代词
            rzs 处所指示代词
            rzv 谓词性指示代词
        ry 疑问代词
            ryt 时间疑问代词
            rys 处所疑问代词
            ryv 谓词性疑问代词
        rg 代词性语素
    m 数词
        mq 数量词
    q 量词
        qv 动量词
        qt 时量词
    d 副词
    p 介词
        pba 介词“把”
        pbei 介词“被”
    c 连词
        cc 并列连词
    u 助词
        uzhe 着
        ule 了 喽
        uguo 过
        ude1 的 底
        ude2 地
        ude3 得
        usuo 所
        udeng 等 等等 云云
        uyy 一样 一般 似的 般
        udh 的话
        uls 来讲 来说 而言 说来

        uzhi 之
        ulian 连 （“连小学生都会”）

    e 叹词
    y 语气词(delete yg)
    o 拟声词
    h 前缀
    k 后缀
    x 字符串
        xx 非语素字
        xu 网址URL
    w 标点符号
        wkz 左括号，全角：（ 〔  ［  ｛  《 【  〖 〈   半角：( [ { <
        wky 右括号，全角：） 〕  ］ ｝ 》  】 〗 〉 半角： ) ] { >
        wyz 左引号，全角：“ ‘ 『
        wyy 右引号，全角：” ’ 』
        wj 句号，全角：。
        ww 问号，全角：？ 半角：?
        wt 叹号，全角：！ 半角：!
        wd 逗号，全角：， 半角：,
        wf 分号，全角：； 半角： ;
        wn 顿号，全角：、
        wm 冒号，全角：： 半角： :
        ws 省略号，全角：……  …
        wp 破折号，全角：——   －－   ——－   半角：---  ----
        wb 百分号千分号，全角：％ ‰   半角：%
        wh 单位符号，全角：￥ ＄ ￡  °  ℃  半角：$