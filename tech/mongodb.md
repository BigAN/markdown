---
title: "mongodb"
date: 2015-03-26 12:00
---
# 基本

[pymongo doc](http://api.mongodb.org/python/current/index.html) 

# 查询

**判断字段为空**

    db.weixin.findOne({""categories":null})

**查询array长度大于1**
    
    1.Using $where
    db.accommodations.find( { $where: "this.name.length > 1" } ); -- 不太好使的说

    2."categories.0":{$exists:false} 不错， false 是《= ，true 是<=


**查询数组**

[参考](http://eksliang.iteye.com/blog/2177292)

查询 数组 按长度 db.weixin.findOne({"categories.0.0":"lvxing"})

 
# 快捷操作

**复制collections**

    db.category_article_cl.find().forEach(function(x){db.category_article_cl_shishang.insert(x)})



# 备份 #

##    mongodump & mongorestore    ##

[copy one collection to another databse ](http://stackoverflow.com/questions/16347134/how-to-use-mongodump-for-1-collection)


恢复数据

    ./mongorestore --db=text_cl_data --collection=category_article_cl -u text_cl_data -p Textcd_pwd2 /home/dongjian/data/text_analysis/category_article_cl.bson
    ./mongorestore --db=text_cl_data --collection=text_cl_data /home/dongjian/data/text_analysis/category_article_cl.bson
    ./mongorestore --db=test -u test -p 1te2st3 --collection=textfea_index /home/dongjian/data/text_analysis/textfea_index.bson

    -b == --db
    -c == --collection

    错误：
        e Oct 29 21:33:23.589 [initandlisten] exception in initAndListen std::exception: locale::facet::_S_create_c_locale name not valid, terminatin
    解决
        export LC_ALL=C
        mongod
    
备份数据

    ./mongodump --db=scrapy --collection=category_article_cl -u scrapy -p scrapy.pwd --out=/home/dongjian/data/text_analysis

复制数据

    scp worddb.bson dongjian@101.251.192.178:/home/dongjian/data/text_analysis

db.category_article_cl_qinggan.find()

# 聚合 #

##      map reduce ##
获取所有collection的name
    
    reduce(
    lambda all_keys, rec_keys: all_keys | set(rec_keys),
    map(lambda d: d.keys(), mongo_db.document.find()),
    set()
    )

# 优化数据库操作 #

> 原则： 对写入操作的优化通常包括减少索引数量及提高`更新效率`。



##      范式化 反范式化##

我的理解.

`范式化` 第三范式，除主键外，数据不能冗余。
`反范式化`  数据冗余，更新复杂。

##      优化文档增长 ##

更新是否会导致体积增长及增长程度。如果增长可预知，可以通过预留足够的增长空间，避免文档移动（当内存块不足以放下内容，会将当前文档移动到末尾，产生内存移动，降低写入速度）。

通过手动填充 -> 在创建文档的时候增加一个大字段，在更新文档的时候删除
    
    db.reviews.update({"_id":id,{$push : {"tags":1},'$unset':{"garbage":true}})

如果文档中有一个字段需要增长，尽量放到garbage（文档最后的位置）之前，这样就不需要对该字段的后面字段进行重写。

##      删除旧数据 ##

1. 固定集合。固定的大小，当达到极限，最旧的一条数据会被pop。
2. TTL 集合。是什么？？？. 写入效率不太高。
3. 多个集合。 每个集合存储一个月的数据。



