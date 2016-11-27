---
title: "yoka"
date: 2015-03-26 11:07
---

[TOC]
# 去重 #
009d8eff-dc6e-4640-8c6c-2d0e18ac3596




## 数据调查 ##

### 启动 check

1. dedup_text.py 是否有limit等。
2. 是否有reset
3. textfeature, dedup_text 是否有错误
4. 是否constant.py 配置正确。
5. textfeature 

### 调查数据原因 ###


    db.sim_group.find({"key_item_time":{$gt:1428312600}}).count()
    db.items.findOne({"_id":ObjectId("553ecee8bd421c6f709719e1")})
    
    db.items.find({},{"content":1})

    db.items.find()

    db.sim_group.findOne({"key_id":"55216feabd421c6f7077da98"})

    db.text_group.findOne({"key_id":"54d35c096bdcdc60488b4600"})
    db.text_group.findOne({"_id":ObjectId("54d35c096bdcdc60488b4600")})

    db.text_profile.findOne({"_id":ObjectId("54d35c096bdcdc60488b4600")})
    
    db.text_group.findOne()
    db.textfea_index.findOne({"group_id":ObjectId("552137ce24f2c149f25651ae")})

    db.text_group.findOne({"key_item._spider.site":"hqrw.com"})

    db.items.findOne({"_spider.site":"hqrw.com"})


    db.items.find({"_spider.ctime":{$gt:143020931}})

    db.items.find({"_spider.site":"www.zjstv.com"})

    db.dedup_log.find({"site":"people.com.cn","ctime":{$gt:1428768000,$lt:1428854399}},{"where":1, "key_id":1})

    db.dedup_lqog.find({"site":"xinmin.cn","ctime":{$gt:1428768000,$lt:1428854399},'where':"simhash_key"})

    db.dedup_log.find({"site":"item.taobao.com","ctime":{$gt:1428163200,$lt:1428249599},'where':"t_key"})

    db.dedup_log.find({"ctime":1428816260})
    slide.ent.sina.com.cn

    db.dedup_log.find({"site":"item.taobao.com","ctime":{$gt:1427817600,$lt:1427903999}},{"where":1,"key_id":1})
    db.dedup_log.find({"site":"zh.moegirl.org","ctime":{$gt:1427904000,$lt:1427990399}},{"where":1,"key_id":1})

    db.variable.update({"key":"sim_mq_time"},{$set:{"value":0}},true)
    db.variable_test.update({"key":"sim_mq_time"},{$set:{"value":0}},true)

    db.text_group.find({"key_item_time":{"$gt":1430064000,"$lt":1430150399}},{"key_item.title":1,'key_item.content':1}).skip(100).limit(5).toArray()
### pickle ###
    import pickle
    i = pickle.load(open("/home/dongjian/data/text_analysis/word_inverted_index_file","r"))
    print len(i)
### 为什么会导致插入了group id 呢？######

### 为什么会略过数据呢？ ###

这说明 nearlist 里面有很多 key_id


### 索引改进？ ####

每次启动重建索引。不在每一次写索引。
### 问题 ###
**未解决问题**
存在多余数据。 --- 数据时间存在更新。 

重复数据。因为分句的改变。 -- 重新过一遍key_id, 去掉last modeify 老的数据。

## 算法 ##

###  weak and ###

lastid 是用来终结循环的。

为什么说idf大能跳的更远？ 考虑只有一个的情况，跳到了lastid，那么再次排序就不需要在考虑这个点。


    testIndex["t0"] = [ 1, 3, 26, 2000000000]
    testIndex["t1"] = [ 1, 2, 4, 10, 100, 2000000000 ]
    testIndex["t2"] = [ 2, 3, 6, 34, 56, 2000000000 ]
    testIndex["t3"] = [ 1, 4, 5, 23, 70, 200, 2000000000 ]
    testIndex["t4"] = [ 5, 14, 78, 2000000000 ]

    sort item
    [1, 't0']
    [1, 't1']
    [1, 't3']
    [2, 't2']
    [5, 't4']

    代码
        #!/usr/bin/env python

    import time
    import heapq
    import pprint
    UB = {"t0": 0.5, "t1": 1, "t2": 2, "t3": 3, "t4": 4}  #upper bound of term's value
    MAX_RESULT_NUM = 5  #max result number


    class WAND:
        #initial index
        def __init__(self, test_index, last_docid):
            self.result_list = []  #result list,(full value , doc id )
            self.invert_index = test_index  #InvertIndex: term -> docid1, docid2, docid3 ...

            self.current_doc = 0
            self.current_invert_index = {}  #posting
            self.query_terms = []
            self.threshold = -1
            self.sort_terms = []
            self.LastID = 2000000000  #big num
            self.last_docid = last_docid

        #get index list according to query term
        def __InitQuery(self, query_terms):
            self.current_doc = -1
            self.current_invert_index.clear()
            self.query_terms = query_terms
            self.sort_terms[:] = []

            for term in query_terms:
                #initial start pos from the first position of term's invert_index
                self.current_invert_index[term] = [self.invert_index[term][0], 0]  #[ docid, index ]

        #sort term according its current posting doc id
        def __SortTerms(self):
            if len(self.sort_terms) == 0:
                for term in self.query_terms:
                    if term in self.current_invert_index:
                        doc_id = self.current_invert_index[term][0]
                        self.sort_terms.append([int(doc_id), term])
            self.sort_terms.sort()

        #select the first term in sorted term list
        def __PickTerm(self, pivot_index):
            return 0

        #find pivot term
        def __FindPivotTerm(self):
            score = 0
            #print "sort term ", self.sort_terms  #[docid, term]

            print "threshold is ",self.threshold
            for i in range(0, len(self.sort_terms)):
                score = score + UB[self.sort_terms[i][1]]
                print 'UB ',self.sort_terms[i][1]," " ,UB[self.sort_terms[i][1]]

                if score >= self.threshold:

                    return [self.sort_terms[i][1], i]  #[term, index]

            return [None, len(self.sort_terms)]

        #move to doc id >= docid
        def __IteratorInvertIndex(self, change_term, docid, pos):
            doc_list = self.invert_index[change_term]
            i = 0
            for i in range(pos, len(doc_list)):
                if doc_list[i] >= docid:
                    pos = i
                    docid = doc_list[i]
                    break

            return [docid, pos]


        def __AdvanceTerm(self, change_index, docid):
            change_term = self.sort_terms[change_index][1]
            pos = self.current_invert_index[change_term][1]
            (new_doc, new_pos) = self.__IteratorInvertIndex(change_term, docid, pos)

            self.current_invert_index[change_term] = [new_doc, new_pos]
            self.sort_terms[change_index][0] = new_doc

        def __Next(self):
            if self.last_docid == self.current_doc:
                print "last_docid == current_doc ",self.last_docid,self.current_doc
                return None

            while True:
                #sort terms by doc id
                self.__SortTerms()

                #find pivot term > threshold
                (pivot_term, pivot_index) = self.__FindPivotTerm()
                print "the pivot is {0}".format(pivot_term)
                if pivot_term == None:
                    #no more candidate
                    print "pivot_term == None"
                    return None

                pivot_doc_id = self.current_invert_index[pivot_term][0]
                print "the pivot doc id  is {0}".format(pivot_doc_id)

                if pivot_doc_id == self.LastID:  #!!
                    print "pivot_doc_id == self.LastID",pivot_doc_id,self.LastID
                    return None
                print "sorted items are:"
                pprint.pprint(self.sort_terms,width=20)
                if pivot_doc_id <= self.current_doc:
                    print "branch 1: pivot_doc_id {0} < = current_doc {1}".format(pivot_doc_id,self.current_doc)
                    print "advanced the 0 th of the sorted item to self.current_doc + 1 -> {0}".format(self.current_doc + 1)
                    change_index = self.__PickTerm(pivot_index)  #always retrun 0 pivot_index is the index of sortitem
                    self.__AdvanceTerm(change_index, self.current_doc + 1)
                else:
                    first_docid = self.sort_terms[0][0]
                    if pivot_doc_id == first_docid:
                        print "branch 2: pivot_doc_id {0} > current doc {1} and pivot_doc_id == first_docid {2}.".format(pivot_doc_id,self.current_doc,first_docid)
                        self.current_doc = pivot_doc_id
                        print "current doc has been changed . then current doc is {0}".format(self.current_doc)
                        return self.current_doc
                    else:
                        #pick all preceding term,advance to pivot
                        print "branch 3: pivot_doc id {0} > current doc {1} and pivot doc id is not the first. advance all the index less than pivot_doc_id.".format(pivot_doc_id,self.current_doc)
                        for i in range(0, pivot_index):
                            change_index = i

                            self.__AdvanceTerm(change_index, pivot_doc_id)

        def __InsertHeap(self, doc_id, score):
            if len(self.result_list) < 3:
                heapq.heappush(self.result_list, (score, doc_id))
            else:
                if score > self.result_list[0][0]:  #large than mini item in heap
                    heapq.heappop(self.result_list)
                    heapq.heappush(self.result_list, (score, doc_id))
            return self.result_list[0][0]

        #full evaluate the doucment, get its full score, to be added
        def __FullEvaluate(self, docid):
            doc_id = docid
            # if doc_vote
            return 4

        def DoQuery(self, query_terms):
            self.__InitQuery(query_terms)
            while True:
                print "###############################################"
                candidate_docid = self.__Next()
                if candidate_docid == None:
                    break
                print "candidate_docid:" + str(candidate_docid)
                #insert candidate_docid to heap
                full_doc_score = self.__FullEvaluate(candidate_docid)
                mini_item_value = self.__InsertHeap(candidate_docid, full_doc_score)
                #update threshold
                self.threshold = mini_item_value
                print "result list ", self.result_list
            return self.result_list


    if __name__ == "__main__":
        testIndex = {}
        testIndex["t0"] = [1, 3, 26, 2000000000]
        testIndex["t1"] = [1, 2, 4, 10, 100, 2000000000]
        testIndex["t2"] = [2, 3, 6, 34, 56, 2000000000]
        testIndex["t3"] = [1, 4, 5, 23, 70, 200, 2000000000]
        testIndex["t4"] = [5, 14, 78, 2000000000]

        testIndex["t0"] = [1, 3, 26]
        testIndex["t1"] = [1, 2, 4, 10, 100]
        testIndex["t2"] = [2, 3, 6, 34, 56]
        testIndex["t3"] = [1, 4, 5, 23, 70, 200]
        testIndex["t4"] = [5, 14, 78]

        last_doc_id = 100
        w = WAND(testIndex, last_doc_id)
        final_result = w.DoQuery(["t0", "t1", "t2", "t3", "t4"])

        print "final result "
        for item in final_result:
            print "doc " + str(item[1])


# 分类 #

##      参考 ##

http://www.blogjava.net/zhenandaci/category/31868.html?Show=All 斯坦福的分类课程，主要讲了one v one，one v rest
http://blog.csdn.net/zhzhl202/article/details/8197109 这个博客讲了基本的内容
http://www.blogjava.net/zhenandaci/category/31868.html?Show=All 

##      数据筛选 ##

##      liblinear 安装 ##

两步make，初始make，使用python文件夹，make


###         调试语句 ###

文章的处理语句

    db.category_article_cl_2.findOne({"_id":ObjectId("5512815673bea0608181f007")})

    db.category_article_cl.update({},{$set:{ "category":0}},false,true)
    db.category_article_cl_2.find({"category":"文化文学"},{"title":1,"svm":1}).sort({"svm":1})

    db.category_article_cl.find({},{"title":1,"svm":1}).sort({"svm":1})

    db.category_article_cl_2.find({"category":""}).count()

    db.category_article_cl_qinggan.find({"category":{$ne:0}}).count()

    db.category_article_cl_qinggan.find({"category":"情感"},{"title":1,"svm":1}).sort({"svm":-1})

    db.category_article_cl_xingzuo.remove({"category":"meishi"})

    db.category_article_cl_qinggan.find({"category":""}).count()

    db.category_article_cl_meishi.find({"svm":{$exists:0}}).count()

    db.category_article_cl.find({},{"title":1,"svm":1}).sort({"svm":1})


    db.category_cl.insert({"title":"萌宠"})


    db.text_cl_data.find().forEach(function(x){db.category_article_cl_meirong.insert(x)})

    db.category_article_cl_2.remove({"category":"非文化文学"})

    db.category_article_cl_2.update({"category":"文化文学"},{$set:{"category":0}},false,true)
    
    db.category_article_cl_youmo.update({"category":"fei_幽默_标注"},{$set:{"category":"幽默"}},false,true)

`调试语句`

    sort -k 2 -n  -t"," keji_result.csv |head -n 3000| awk -F "," '{if($2>0.15){print $1,$2,$3}}'

##      模型上线    ##

mongo 10.0.192.10:37017/cache

**重命名文件 上线** 

    ls *.model | awk -F '[_|.]' '{print $0,"model_"$1"#"$2"_0"}'| xargs -n 2 cp
    #ls *_all_train_feature_dict | awk -F '_' '{print $0,"feature_"$1"#"$2"_0"}'| xargs -n 2 cp 不用了。
    ls model_* | awk -F "[_|#]" '{print $2"_"$3"_all_train_feature_dict"}'|awk -F '_' '{print $0,"feature_"$1"#"$2"_0"}'|xargs -n 2 cp

    cp model_*keji* /home/dongjian/data/text_analysis/classification_online/models 
    cp model_* /home/dongjian/data/text_analysis/classification_online/models 
    cp feature_* /home/dongjian/data/text_analysis/classification_online/models 
    

    ls model_*| cut -c 7- | xargs -n 1 echo feature_$1| awk -F ' ' '{print $1$2}' |


    #onevrest
    ls model_* | awk -F "[_|#]" '{print $2"_"$3"_all_train_feature_dict"}'|awk -F '_' '{print $0,"feature_"$1"#"$2"_0"}'|xargs -n 2 cp

    ls *.model | awk -F '.' '{print $0" model_"$1"_0"}'| xargs -n 2 cp
    ls *_all_train_feature_dict | awk -F '_' {'print $0" feature_"$1"_0"'}| xargs -n 2 cp



__查看模型的model准确率。__

    cat *mengchong*log|grep -E 'svm|Accuracy|pos|neg'
__查看错误分类结果__

    cat tmp |awk -F "\t" 'BEGIN{sum=0}{print $2,sum;sum=$2+sum}END{print sum}'

__模型生成__
    
    add_one.sh 对目标类型的所有分类进行训练
    复制models ls *.model | awk -F '[_|.]' '{print $0,"model_"$1"#"$2"_0"}'| xargs -n 2 cp
    重命名后，delete_extra_model.py 进行删除
    复制features ls model_* | awk -F "[_|#]" '{print $2"_"$3"_all_train_feature_dict"}'|awk -F '_' '{print $0,"feature_"$1"#"$2"_0"}'|xargs -n 2 cp
    copy文件，上线。
        cp model_* /home/dongjian/data/text_analysis/classification_online/models 
        cp feature_* /home/dongjian/data/text_analysis/classification_online/models 

##  分析结果 ##

    db.category_article_cl_meishi.find({"result":{$exists:1}},{"result_all":0}).toArray()


    db.weixin.find({},{"categories":1,"title":1,"trim_content":1}).skip(0).limit(10).toArray()
    
    db.weixin.findOne(ObjectId("552ddc85bd421c6f7083e7b5"),{"main":0,'msgext':0})

    db.weixin.findOne(ObjectId("54b216bc51ae65e634389434"))

    db.weixin.findOne({"categories":{$exists:0}})

    db.weixin.findOne(ObjectId("5562d4ba73bea0635409e5f3"))

    db.weixin.findOne({"":{$exists:1}})

    db.weixin.find({},{"title":1,"categories":1}).sort({"_id":-1})

    db.weixin.find({"title":/本该如此/},{"categories":1,"title":1})

    db.weixin.findOne({"title":{"$regex":"我们只剩下"}},{"categories":1,"title":1})

**微信数据未分类**
微信时间筛选，类别长度为0.

    db.weixin.find({"main.create_time":{"$gt":1434816000},"categories.0":{$exists:false},"categories":{$exists:1}},{"categories":1})
    
## badcase
    db.category_article_cl_keji.update({"_id":ObjectId("54b57b8851ae65e6343896cc")},{"$set":{"category":"feiadd"}})

删除一个分类的所有文件

    ls * | grep shizhuang | xargs -n 1 rm 



拷贝模型

    cp feature_*  /home/dongjian/data/text_analysis/classification_online/models

    cp model_*  /home/dongjian/data/text_analysis/classification_online/models



# 文章时效性 

# 推荐

click_shown 频次 统计

    cat log_20150611 |awk -F , '{print $1,$2,$3,substr($NF,0,5)}'> all
    cat all | awk '{if($2=="shown"){$2="";print $0}}' > shown
    cat all | awk '{if($2=="click"){$2="";print $0}}' > click
    cat shown|sort| uniq
    cat click|sort| uniq
    cat shown_uniq click_uniq | sort | uniq -d > result # 取两者的交集。
##  上线流程 
    自己本机测试。
    自己本机test_api。
    在online 上。test_api

#日志
获取日志错误

    cat data_parse_log| grep ERROR| grep -v tracks | cut -c 27-| sort |uniq -c


#lTR 

##  模型训练

    java -jar RankLib-2.1-patched.jar  -load listnet_model -rank test.da.rs -score listnet_myscorefile.txt #冲排序
    sh paste_files.sh test.da.rs lambdamart_myscorefile.txt predict.rs.lambdamart # 生成true prdict组合文件
    sh cal_auc.sh predict.rs.lambdamart # 计算auc

