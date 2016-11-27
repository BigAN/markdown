---
title: "python"
date: 2015-03-28 12:55
---
关于python syspath
    

[TOC]

# Python 语法相关

##IDE
        ○ pycharm 破解
            § http://sjolzy.cn/Pycharm-crack-Pycharm-serial-number.html
        ○ python -V 查看版本
            
##基础数据结构

### 查看属性 

print haha

### tuple ###
                • 构建tuple的基本是逗号，因为括号的优先级更高(瞎扯)
                        □ 所以(1) 是一个int
                        □ (1,) 是一tuple
### List 
                • 左闭右开
                • 清空u
                        □ del list[:]z
                        □ a=[]
                        □ 这两种方式的区别
                                1 大数据量的list，要进行局部元素删除，尽量避免用del随机删除，非常影响性能，如果删除量很大，不如直接新建list，然后用下面的方法释放清空旧list。
                                
                                2 对于一般性数据量超大的list，快速清空释放内存，可直接用 a = [] 来释放。其中a为list。
                                
                                3 对于作为函数参数的list，用上面的方法是不行的，因为函数执行完后，list长度是不变的，但是可以这样在函数中释放一个参数list所占内存： del a[:]，速度很快，也彻底：）
                        
                • 用某个固定值初始化列表
                initial_value = 0
                list_length = 5
                sample_list = [ initial_value for i in range(10)]
                sample_list = [initial_value]*list_length
                list
                • 便捷函数
                        □ zip
                        □ reverse()
                                § return None，直接修改原
                        □ append() 追加元素
                        □ insert(index,var)
                        □ remove(var) 删除第一次出现的该元素,var 为该元素
                        □ index( var) 寻找var， 如果没有寻找到则抛出异常。
                        □ +=, 合并列表(注意后面必须为列表，int 会报错误 xx is not iterable)
                        □ 
list comprehansion

在list comprehansion 中使用 if else

    rs = lambda x:[x if x == i else 3 for i in range(1,10) if i ==3 ]

### string 
                • 方法
                        □ S.find(substring, [start [,end]]) #可指范围查找子串，返回索引值，否则返回-1
                        □ S.rfind(substring,[start [,end]]) #反向查找
                        □ S.index(substring,[start [,end]]) #同find，只是找不到产生ValueError异常
                        □ S.rindex(substring,[start [,end]])#同上反向查找
                        □ S.count(substring,[start [,end]]) #返回找到子串的个数
                        S.lowercase()
                        S.capitalize()      #首字母大写
                        S.lower()           #转小写
                        S.upper()           #转大写
                        S.swapcase()        #大小写互换
                        S.split(str, ' ')   #将string转list，以空格切分
                        S.join(list, ' ')   #将list转string，以空格连接
                        处理字符串的内置函数
                        len(str)                #串长度
                        cmp("my friend", str)   #字符串比较。第一个大，返回1
                        max('abcxyz')           #寻找字符串中最大的字符
                        min('abcxyz')           #寻找字符串中最小的字符
                        str.strip("xyz") 从字符串的前端和后端一起去掉，匹配串中的内容，从前后开始扫描，判断是否在前后两端。
                        
                字符串效率
                    a += b 10**3 的复杂度是N*2
                    ''.join([a,]*1000) 的复杂度是n
                    所以 join 是快的在字符串比较多的情况下 
### Dict ###
                § items()
                        □ 转换为列表。在排序的时候可以用。
                § keys() 获得键值
                § 遍历dict
                        For d,k in d:
                                Print d,k( actully is the key and value)
orderdict 。。。。。。。。。。≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥≥
#### dict 操作 ####  
    合并dict 
        a.update(b)
        dict(a.items()+b.items())
        dict(a,**y)


                        
        
### set  
                python的set和其他语言类似, 是一个无序不重复元素集, 基本功能包括关系测试和消除重复元素. 集合对象还支持union(联合), intersection(交), difference(差)和sysmmetric difference(对称差集)等数学运算.
                
                sets 支持 x in set, len(set),和 for x in set。作为一个无序的集合，sets不记录元素位置或者插入点。因此，sets不支持 indexing, slicing, 或其它类序列（sequence-like）的操作。
                
                 
                
                下面来点简单的小例子说明把。
                
                >>> x = set('spam')
                >>> y = set(['h','a','m'])
                >>> x, y
                (set(['a', 'p', 's', 'm']), set(['a', 'h', 'm']))
                
                再来些小应用。
                
                >>> x & y # 交集
                set(['a', 'm'])
                
                >>> x | y # 并集
                set(['a', 'p', 's', 'h', 'm'])
                
                >>> x - y # 差集
                set(['p', 's'])
                
                记得以前个网友提问怎么去除海量列表里重复元素，用hash来解决也行，只不过感觉在性能上不是很高，用set解决还是很不错的，示例如下：
                
                >>> a = [11,22,33,44,11,22]
                >>> b = set(a)
                >>> b
                set([33, 11, 44, 22])
                >>> c = [i for i in b]
                >>> c
                [33, 11, 44, 22]
                
                很酷把，几行就可以搞定。
                
                1.8　集合 
                 
                集合用于包含一组无序的对象。要创建集合，可使用set()函数并像下面这样提供一系列的项：
                
                 
                
                s = set([3,5,9,10])      #创建一个数值集合
                
                t = set("Hello")         #创建一个唯一字符的集合
                
                 
                
                与列表和元组不同，集合是无序的，也无法通过数字进行索引。此外，集合中的元素不能重复。例如，如果检查前面代码中t集合的值，结果会是：
                
                 
                
                >>> t
                
                set(['H', 'e', 'l', 'o'])
                
                 
                
                注意只出现了一个'l'。
                
                集合支持一系列标准操作，包括并集、交集、差集和对称差集，例如：
                
                 
                
                a = t | s          # t 和 s的并集
                
                b = t & s          # t 和 s的交集
                
                c = t – s          # 求差集（项在t中，但不在s中）
                
                d = t ^ s          # 对称差集（项在t或s中，但不会同时出现在二者中）
                
                 
                
                基本操作：
                
                t.add('x')            # 添加一项
                
                s.update([10,37,42])  # 在s中添加多项
                
                 
                
                使用remove()可以删除一项：
                
                t.remove('H')
                
                 
                
                len(s)
                set 的长度
                
                x in s
                测试 x 是否是 s 的成员
                
                x not in s
                测试 x 是否不是 s 的成员
                
                s.issubset(t)
                s <= t
                测试是否 s 中的每一个元素都在 t 中
                
                s.issuperset(t)
                s >= t
                测试是否 t 中的每一个元素都在 s 中
                
                s.union(t)
                s | t
                返回一个新的 set 包含 s 和 t 中的每一个元素
                
                s.intersection(t)
                s & t
                返回一个新的 set 包含 s 和 t 中的公共元素
                
                s.difference(t)
                s - t
                返回一个新的 set 包含 s 中有但是 t 中没有的元素
                
                s.symmetric_difference(t)
                s ^ t
                返回一个新的 set 包含 s 和 t 中不重复的元素
                
                s.copy()
                返回 set “s”的一个浅复制
                
                
                请注意：union(), intersection(), difference() 和 symmetric_difference() 的非运算符（non-operator，就是形如 s.union()这样的）版本将会接受任何 iterable 作为参数。相反，它们的运算符版本（operator based counterparts）要求参数必须是 sets。这样可以避免潜在的错误，如：为了更可读而使用 set('abc') & 'cbs' 来替代 set('abc').intersection('cbs')。从 2.3.1 版本中做的更改：以前所有参数都必须是 sets。
                
                另外，Set 和 ImmutableSet 两者都支持 set 与 set 之间的比较。两个 sets 在也只有在这种情况下是相等的：每一个 set 中的元素都是另一个中的元素（二者互为subset）。一个 set 比另一个 set 小，只有在第一个 set 是第二个 set 的 subset 时（是一个 subset，但是并不相等）。一个 set 比另一个 set 打，只有在第一个 set 是第二个 set 的 superset 时（是一个 superset，但是并不相等）。
                
                子 set 和相等比较并不产生完整的排序功能。例如：任意两个 sets 都不相等也不互为子 set，因此以下的运算都会返回 False：a<b, a==b, 或者a>b。因此，sets 不提供 __cmp__ 方法。
                
                因为 sets 只定义了部分排序功能（subset 关系），list.sort() 方法的输出对于 sets 的列表没有定义。
                
                
                运算符
                   运算结果
                
                hash(s)
                   返回 s 的 hash 值
                
                
                下面这个表列出了对于 Set 可用二对于 ImmutableSet 不可用的运算：
                
                运算符（voperator）
                等价于
                运算结果
                
                s.update(t)
                s |= t
                返回增加了 set “t”中元素后的 set “s”
                
                s.intersection_update(t)
                s &= t
                返回只保留含有 set “t”中元素的 set “s”
                
                s.difference_update(t)
                s -= t
                返回删除了 set “t”中含有的元素后的 set “s”
                
                s.symmetric_difference_update(t)
                s ^= t
                返回含有 set “t”或者 set “s”中有而不是两者都有的元素的 set “s”
                
                s.add(x)
                
                向 set “s”中增加元素 x
                
                s.remove(x)
                
                从 set “s”中删除元素 x, 如果不存在则引发 KeyError
                
                s.discard(x)
                
                如果在 set “s”中存在元素 x, 则删除
                
                s.pop()
                
                删除并且返回 set “s”中的一个不确定的元素, 如果为空则引发 KeyError
                
                s.clear()
                
                删除 set “s”中的所有元素
                
                
                请注意：非运算符版本的 update(), intersection_update(), difference_update()和symmetric_difference_update()将会接受任意 iterable 作为参数。从 2.3.1 版本做的更改：以前所有参数都必须是 sets。
                
                还请注意：这个模块还包含一个 union_update() 方法，它是 update() 方法的一个别名。包含这个方法是为了向后兼容。程序员们应该多使用 update() 方法，因为这个方法也被内置的 set() 和 frozenset() 类型支持。
                 
                 
                
                
        堆栈 
                • what: 就是基本的队列可以当做堆栈来使用
                • how:
                        ○ 实现了pop和append 方法(push)
                        
        队列
                • what:通过from collections import deque实现
                • how:
                        ○ 初始化需要deque([1,2,3,])
                        ○ 实现了append 。即为增加
                        ○ pop()pop出最右边的。popleft()pop 最左边的。
        
        
        
        
        
        ○ 
        ○ List 
    • python 基本语法
        ○ print 基本
            § 格式:print "  % " % (,,,)
            § 字符串 %s
            § 16 X 
            § 格式化输出float
            import math#default
            print "PI = %f" % math.pi#width = 10,precise = 3,align = left
            print "PI = %10.3f" % math.pi#width = 10,precise = 3,align = rigth
            print "PI = %-10.3f" % math.pi#前面填充字符
            print "PI = %06d" % int(math.pi) 
            § 格式化string
                
                print "%.3s " % ("jcodeer")#precise = 4
                print "%.*s" % (4,"jcodeer")#width = 10,precise = 3
                print "%10.3s" % ("jcodeer")
            § 赋值操作
                □ what
                    ® 是改变链接的指向。
                        list="hehe"
                        emp=list
                        emp=[]
                            } 这里是不能清空list的。因为改变的是链接。
                            } 
                            } 

## python 基本计算 ##
        ○ python 在负数除中的变化， 6/-132 = -0.0455 -1 在 java 中，6/-132 = 0
            § a/b+1 if a%b!=0 and a/b<0 else a/b
        ○ n次方
            § print 10**n
        ○ 排序
            § 基本
                □ l.sort() -- 按照第一个属性排序 列表
                    a) 定义cmp 为比较函数
                        ◊ def mycmp(a,b)
                            return cmp(a.lower(),b.lower())
                        ◊ i.sort(lambda x,y:cmp(x[2],y[2]))
                □ sorted() -- 第一个参数为目标，第二个参数为key(key=str.lower)
                
                □ 通过装饰器实现多属性的排序
                    ® 比如
                        ◊ i=["a123","b245","c423"]
                        ◊ 按照第二个字母排序
                        ◊ tmp_i=[(x[1],x) for x in i]
                        ◊ tmp_i.sort()
                        ◊ i=[x[1] for x in i]
                        
                □ dict 字典排序
                    ® 通过items 转为list 来排序。
                    ® 使用sorted. 用lamdba 函数来作为.
                        >>> sorted(mydict.items(), key=lambda d:d[0])  
                        [('A01', 'first'), ('A14', 'second'), ('Aa1', 'third')]  
                        >>> mydict = {"A01":"first", "A14":"second", "Aa1":"third"}  
                        >>> sorted(mydict.items(), key=lambda d:d[0])  
                        [('A01', 'first'), ('A14', 'second'), ('Aa1', 'third')]  
                        >>> sorted(mydict.items(), key=lambda d:d[1])  
。                        [('A01', 'first'), ('A14', 'second'), ('Aa1', 'third')]  
                        >>> print mydict  
                        {'A14': 'second', 'A01': 'first', 'Aa1': 'third'}  
                □ 
                □ 对象排序
                    ® 使用lamdba 来实现cmp 函数
                        ◊ obj_list.sort(lambda x,y: cmp(x.a, y.a)) #按对象的a属性进行排序 
                □ 字典列表
                    input = [{'name': 'Homer', 'age': 39}, {'name': 'Bart', 'age':10},{'name': 'Wang', 'age':10},{'name': 'Ab', 'age':10}]  
                    print input  
                    input.sort(lambda x,y : cmp(x['name'], y['name'])) 
                    ® 逆向排序
                        ◊ input.sort(lambda x,y : -cmp(x['name'], y['name']))
                □ 多级排序
                    ® 使用operater.itergetter,attrgetter 的函数
                        ◊ 返回值是个函数，比如itemgetter(2)， 返回的是获得第二域的函数。既b([1,2,3]) 为3
                        
                □ 大数据排序
            § 排序效率
                □ 一般不使用cmp,因为需要比较多次。一般写key的lambda
                    a) 通常, key 和 reverse 比 cmp 快很多, 因为对每个元素它们只处理一次; 而 cmp 会处理多次.  
                    也就是说, 同等情况下, 写 key 函数比写 cmp 函数要高效很多.  
                
## 函数式 编程 ##
    
    函数式编程
    链接:
        http://blog.sina.com.cn/s/blog_6d312b310100ul58.html 讲了 基本的函数式编程的特征 & python对于函数式编程的支持
    where: 区别于过程式编程。
        

    filter,reduce,map...
            ® filter(bool_func, seq)
                1. >>> filter(lambda x : x%2 == 0,[1,2,3,4,5])  
                2. [2, 4]  
            ® map(func,seq) = func*sql
                1. >>> map(lambda x : x * 2,[1,2,3,4])  
                2. [2, 4, 6, 8]  
            ® reduce
                □ 很奇怪不知道干啥的。说白了两步，
                    ® reduce(lambda x,y:x+y,[1,2,3,4,5],2)
                    =(1+2)+3)+4)+5
                    第一步 1 + 2 获得一个结果然后再继续迭代

    
    • and or 
        ○ and:真才走 (0 ''、[]、()、{}、None 等一切能表达空的东西 为假 )
            § print 1 and 2
                □ 2
            § print 0 and 2
                □ 0
        ○ or:假才走
            § print 1 or 2 
                □ 1
            § print 0 or  2
                □ 2
        ○ 应用
            § protocol = secure and "https://secure" or "http://www"
                □ secure 为是否采用https 
                    ® 如果采用 则第一个参数为真 往后走 返回 “https://” 同时这个为真 返回 “https：//”
                    ® 如果不采用 则为否 不往后走 返回 0  0 or "http://www" 0 为假 往后走 
        ○ 注意
            § 0> None and 0 or None 
                □ 这是不行的。因为  0>None and 0 的值 不管怎样都是  false 所以 or None 一定是 None
                
    • Try-else 语法
            try:
                operation_that_can_throw_ioerror()
            except IOError:
                handle_the_exception_somehow()
            else:
                 # we don't want to catch the IOError if it's raised
                another_operation_that_can_throw_ioerror()
            finally:
                something_we_always_need_to_do()
        1.else 只有在try正常运行没有ioerror的时候运行
        2.else 在fananlly 前面运行
        3.在else 里面没有error 被抓住。
## 正则表达式 ##

正则表达式中，group（）用来提出分组截获的字符串，（）用来分组
    
    import re
    a = "123abc456"
    print re.search("([0-9]*)([a-z]*)([0-9]*)",a).group(0)   #123abc456,返回整体
    print re.search("([0-9]*)([a-z]*)([0-9]*)",a).group(1)   #123
    print re.search("([0-9]*)([a-z]*)([0-9]*)",a).group(2)   #abc
    print re.search("([0-9]*)([a-z]*)([0-9]*)",a).group(3)   #456
    

究其因

1. 正则表达式中的三组括号把匹配结果分成三组

        •  group() 同group（0）就是匹配正则表达式整体结果
        •  group(1) 列出第一个括号匹配部分，group(2) 列出第二个括号匹配部分，group(3) 列出第三个括号匹配部分。

2. 没有匹配成功的，re.search（）返回None

3. 当然郑则表达式中没有括号，group(1)肯定不对了。

正则的match对象会被缓存，所以没必要先match，在来匹配。

正则技巧
    
    一、正则基本语法

    1. 正则匹配默认为贪婪模式，即尽可能多地匹配：

       'abdba'.match(/.*b/)结果为abdb   
    
       在通配符后加 '?' 表示非贪婪匹配，即尽可能少地匹配
       'abdba'.match(/.*?b/)结果为ab
    
       注意多个元字符同时存在匹配时，前面的匹配尽可能多：
       'abdba'.match(/(\w+)(\w+)/)结果为["abdba","abdb","a"]
    
    2. 正则中|分隔符最优先进行分隔
       /^a(bc)|(cd)e$/ 等价于 /(^abc)|(cde$)/
    
       注意没有进行匹配的子表达式内的分组结果为undefined：
       'abc'.match(/abc(.*)|a(\w+)/)结果为["abc","",undefined]
    
       其中第一个子表达式abc(.*)匹配成功，分组无匹配，结果是""
       第二个子表达式a(\w+)未进行匹配，分组结果是undefined
    
    3. ^和$代表行首和行尾字符，因此有这样的正则：
       location.search.match(/para=(\d+)(&|$)/)
    
    4. ?:组合使用，代表该分组为非捕获分组，即在匹配结果中不编号输出:
       '?para=20'.match(/para=(\d+)(&|$)/)结果为["para=20","20",""]
       而非捕获分组结果如下：
       '?para=20'.match(/para=(?:\d+)(&|$)/)结果为["para=20",""]
    
    5. \n可以将已匹配得到的第n个分组结果作为匹配项：
       /(\d)\w+\1/.test('1abc1')结果为true
       /(\d)\w+\1/.test('1abc2')结果为false
    
    6. 预匹配，有肯定(?=x)和否定(?!x)两种形式，表示匹配结果后紧跟着x或不能有x（注意匹配结果中不含x）：
       'abc'.match(/\w/g)结果为["a","b","c"]
       'abc'.match(/\w(?=b)/g)结果为["a"]
       'abc'.match(/\w(?!b)/g)结果为["b","c"]
       预匹配分为向前查看和向后查看，JS目前只支持向前查看（即匹配项还没匹配到的部分，对应字符串更后的位置），向后查看的正则形式为(?<=x)和(?
    二、正则相关函数

    1. String.replace,该函数结合正则主要有以下三种用法(注意该函数返回新字符串而不会修改字符串本身)：
       a.基本替换，注意不加g的话找到一个匹配替换就会停止
       '?para=20&value=9'.replace(/\d+/g,'0') 结果为 "?para=0&value=0"
       b.获取分组，在替换字符串中$n代表第n个捕获分组，从0开始计数
       '?para=20&value=9'.replace(/para=(\d+)&value=(\d+)/,'para:$2|value:$1') 结果为 "?para:9|value:20"
       c.第二个参数为函数时，该函数参数依次为各个捕获分组(string)，之后是匹配项在字符串中出现的位置(number)和原字符串的副本
       '?para=20&value=9'.replace(/para=(\d+)&value=(\d+)/,function(p0,p1,p2,p3,p4){
          return 'res=' + (Number(p1)-Number(p2));
       }) 结果为 "?res=11"
注意
    
    这里的group 和 groups 有所不同。group会返回所有匹配结果。而groups只有在正则表达式中定义了分组才会被显示。
    例子：
        In[20]: re.search('\d',"t1").groups()
        Out[20]: ()
        In[21]: re.search('\d',"t1").group()
        Out[21]: '1'
        In[22]: re.search('(\d)',"t1").group()
        Out[22]: '1'
        In[23]: re.search('(\d)',"t1").groups()
        Out[23]: ('1',)
多个正则写法技巧

    def trim_content(content):
    pats = [
        r'\[img\].*?\[/img\]'  # 去除图片标签
        , r'\s+'  #  去除回车换行等空白符
    ]
    for p in pats:
        content = re.sub(p, '\t', content)
    return content.strip()

## python 其他 ##
    • python 的三元表达式
        ○ var= x if exper else b
        ○ var = exper and b or c 
    • Lambda:
        定义
                g=lamdba x: x**2 相当于
                Def f(x): return x**2
        调用
                Print g(4)
        If else:
                Lambda x: x if(x>3) else None  
                Note: else None 必须有
        有意思的东东
                fs = [(lambda n: i + n) for i in range(10)]
                这里实际是产生了10个lamdba函数
                目的是 
                Fs[3](4)=7 但是结果是 13 
                这是因为i已经执行完了， i使用的是匿名函数外的全局变量。
                所以调用的值是执行完的。所以这里注意使用全局的变量时，使用赋值方式。
                fs = [(lambda n: i=i + n) for i in range(10)]
                正确答案
                
                
        问题：
                1. 在lambda 里可以用for 么
                        a. 这里不能使用for。可以用 [] 来代替。
                
        
    • __name__:
        __main__
        1. 如果模块是被导入，__name__的值为模块名字
        2. 如果模块是被直接执行，__name__的值为’__main__’
    • 
    • Switch 实现：
        ○ A.使用dictionary
        values = {
                   value1: do_some_stuff1,
                   value2: do_some_stuff2,
                   ...
                   valueN: do_some_stuffN,
                 }
        values.get(var, do_default_stuff)()
        ○ B.使用lambda
        result = {
          'a': lambda x: x * 5,
          'b': lambda x: x + 7,
          'c': lambda x: x - 2

    }[value](x)
    
    ○ 实现1： beautiful  implement 
        # This class provides the functionality we want. You only need to look at
        # this if you want to know how this works. It only needs to be defined
        # once, no need to muck around with its internals.
        class switch(object):
            def __init__(self, value):
                self.value = value
                self.fall = False
            def __iter__(self):
                """Return the match method once, then stop"""
                yield self.match
                raise StopIteration
            def match(self, *args):
                """Indicate whether or not to enter a case suite"""
                if self.fall or not args:
                    return True
                elif self.value in args: # changed for v1.5, see below
                    self.fall = True
                    return True
                else:
                    return False
        # The following example is pretty much the exact use-case of a dictionary,
        # but is included for its simplicity. Note that you can include statements
        # in each suite.
        v = 'ten'
        for case in switch(v):
            if case('one'):
                print 1
                break
            if case('two'):
                print 2
                break
            if case('ten'):
                print 10
                break
            if case('eleven'):
                print 11
                break
            if case(): # default, could also just omit condition or 'if True'
                print "something else!"
                # No need to break here, it'll stop anyway
    • Range 和xrange  和 reverse
        ○ xrange 
            § xrange(1, 10, 2)
        ○ reverse 反转
        ○ 都是用在循环的时候使用，
            for i in range(0, 100):
            print i
             
            for i in xrange(0, 100):
            print i
        ○ 区别
            § Range 生成一个列表
            § Xrange 每回返回一个值
                □ A=range(0,100)
                □ A=xrange(0,100)
                □ Print type(a)
                □ Print a
        ○ 注意
            § 不包括100  为[a,b)
        ○ 使用xrange
        § 使用需要迭代序列的一部分。在这种情况下，仅需要迭代序列切片就可以实现，注意添加必要的注释注明用意：
        for word in words[1:]: # 不包括第一个元素
    print word
        有一个例外：当你迭代一个很大的序列时，切片操作引起的开销就比较大。如果序列只有10个元素，就没有什么问题；但是如果有1000万个元素时，或者在一个性能敏感的内循环中进行切片操作时，开销就变得非常重要了。这种情况下可以考虑使用xrange代替range [1]。
        
    • Round 
        ○ 保留两位小叔
    • 文件编码
        ○ # coding=utf-8
        ○ 编码
            ○ .decode('utf-8' ).encode('GBK')
        
    • 全局变量
        ○  global variable
        ○ 避免使用全局变量
            § 解决 使用全局变量在一个模块内。
    • 判断
        ○ 判断是否为空
            § list=[]
                □ if not list : 判断是否为空
        ○ 判断一致 is ==  &
            § == 判断值相等
            § Is 地址是否相同(x=y)
    • assert语法相关
        ○ 判断条件，assert  条件，如果不在其中，则退出
    • 将列压缩到一起,返回第一个元素的元祖
        ○ Eg
            Zip(ages,name)
                    For names,age in zip(names,ages):
                    
            需要同时迭代两个循环，用同一个索引来获取两个值。这种情况下，可以用zip来实现：
            for word, number in zip(words, numbers):
    print word, number
            
                    
    • string 方法
        ○ index. 
            § str.index(str,start,end)
                □ 返回位置
    • Enumberate()
        ○ 在for index, I in enumberate(words)
        ○ 使用索引
    • Reversed() 和sorted 翻转和迭代，对副本进行操作，原数据不便
    • 列表推导：这个比较牛逼
        ○ Eg1: x*x for x in range(10)
        ○ 条件if,for:    x*y for x in range(10) for y in range(10)
        ○ 注意加上执行 []
            § [i*I for i in xrange(10)]
    • 关于del 
        ○ Python 对象管理机制: 当没有变量指向的时候，释放。
        ○ Del 作用: 删除引用 ， 也删除名字。
        ○ 本质是 对象  名字 引用 
            § 有对象 名字  b=a=[0] a=none 这个时候 ，a之前对应的对象，名字 都存在
            § 只有对象 b=a=[0] del a  这个时候 只有b和[0]存在
    • 关于eval
        ○ 字符串作为参数 eval('3+4') 并返回表达式的值
        ○ 相对应的 exec 用来执行字符串中 Python的命令 exec 'hello world'
    • Ord(a)
        ○ 返回单字符的 asc码值。
    • 字典操作
        ○ kwargs.pop("product", None) 获得product键值对应的值,并消除
    • 字符串替换
        ○ 1是用字符串本身的方法。
            § a = 'hello word'
            § a.replace('word','python')
        ○ 2用正则来替换字符串
            import re
            strinfo = re.compile('word')
            b = strinfo.sub('python',a)
            print b
            输出的结果也是hello python
            
    • 正则表达式
        ○ match
            § 从起点开始搜
    • 使用DECIMAL
        ○ 设置位数
            § 两个参数 import getcontext,Decimal
                □ con.prec 使用来制定位数的但是我试验发现不好使。how:con.prec=5 表达5位
                    ® 原因是这个设置位数只在操作的时候才生效。
                    
                    >>> from decimal import getcontext, Decimal
    >>> getcontext().prec = 6
    >>> Decimal('50.567898491579878')
    Decimal('50.567898491579878')
    >>> # Shouldn't that have been rounded to 6 digits on instantiation?
    >>> Decimal('50.567898491579878') * 1
    Decimal('50.5679')
    >>> # Instead, it only follows my precision setting set when operated on.
    >>> 
            
            § 使用Decimal('50.5679').quantize(Decimal('0.00'))形式
                □ 这样规定的是小数的位数经测试。
                
            § 还有一种取巧的方法
                □ >>> print "%.2f" % a  
                □ i= "%.2f" % a 
                □ 13.95
    • 
`Python  tricks `
    
    生成长度100的且为空格的字符串。
        ○ " "*100
    • 去掉print 的换行
        ○ Python 2：使用print后加一个逗号：print 'hello',
        Python 3：输入参数end：print ('hello', end='')
     


python 数据结构操作

`python dict`
 
    • python get
        ○ use:dict.get("c","none") # dict={'c':"nihao"}  answer is nihao
        ○ what:Return the value for key if key is in the dictionary, else default. If default is not given, it defaults to None, so that this method never raises a KeyError.
    • QueryDict
        ○ a http request object which is imuttable
        ○ use:
            § handle it in shell
                □ from django.http import QueryDict
                □ from django.conf import settings
                □ settings.configure
_______________________________________________________________________________________________________

`Python 数学方法`

    • 绝对值
        ○ abs

`Python 路径`

    • 路径相关操作
        ○ 打印当前python 路径
            § sys.executable
    常用path 方法
    os.path.walk
    os.path.dirname
    os.path.abspath
    os.path.realpath


    获得路径的父路径

    os.path.abspath(os.path.join(os.getcwd(),*[os.pardir]*3))
    获得当前文件的路径
        f you mean the directory of the script being run:

        import os
        os.path.dirname(os.path.abspath(__file__))
    • SYSPATH
        ○ 怎么运转的？
            § 什么时候会自动添加
                □ 在python xxx.py 的时候会自动加载当前路径作为syspath。
                    #dongjian/a.py
                    def pMe():
                            print 'a.pyt'
                    #dongjian/b.py 
                    import a.py
                    def pMeb():
                            print ' b.pyt'
                    print pMe()
                    print pMeb()
                    #path dongjian/
                            python b.py -- right
                    #path /
                            pathon b.py --wrong . import error no a module
                    
                    
                
            § 什么时候会需要添加？怎么添加？
                □ 放到site-packages 下面，python会将下面的site-packages下面的所有子文件夹作为syspath
                □ 新建在site-packages下面新建.pth  加入路径
                □ 使用PYTHONPATH 环境变量
                    ® export PYTHONPATH=$PYTHONPATH:/home/caoxin/pythonshell/config
                □ 使用sys.path.insert(0,'/cdm/')
## Python字符编码 字符集 ##

    参考链接
        • http://www.jb51.net/article/26543.htm 和 http://www.cnblogs.com/huxi/archive/2010/12/05/1897271.html
        • BOM 软件在文件开始的时候会插入三个字符，来表示编码格式。
        • 文件编码格式
                ○ s="哈哈"
                ○ print repr(s)
                ○ 如果文件是utf8则s就是utf8，如果是gbk就是gbk
        • 声明编码格式
                ○ #coding utf-8 这里python 只看是否有 # coding和编码（utf -8）
                ○ 声明编码格式的作用是在定义unicode的时候，起到从文件编码转码为unicode的编码格式。
                ○ 高级ide，会将文件格式编码默认为文件的声明编码格式。
        • 转码出错
                ○ 一般是系统的默认编码为ascii （或者声明编码格式）,当
                        • pr="哈哈"--gbk
                        • pr.encode("utf-8) 
                                □ 会报错，因为把gbk转为utf8的过程会由系统先将gbk通过ascii 转为unicode，在变成utf-8.
                ○ 文件编码和声明编码转码错误
                        • # coding utf 8 
                        • # 文件编码格式为gbk
                        • pr=u"哈哈"
                        • print repr(ss)
                                □ 报错因为，这里从文件编码转为unicode过程分了几部。
                                        ® 第一步 获取系统编码格式，这里保存为gbk就是gbk
                                        ® 第二部 将gbk的格式转换为unicode，这里的转码格式是utf8就是声明格式。
                                        ® 因为utf8 表中不存在该字符则报错。
                        
        • str 和unicode 都是basestring的子类。
                ○ str其实是字符串是由unicode编码的字节(这个编码可能是Utf-8,gbk还是什么)组成的字符串。
        • .decode('utf-8' ).encode('GBK')
                ○ 这种的应用情况是当原始字符为utf-8的编码，通过decode来解析成unicode，再通过编码为gbk.
        • 系统带入方法
                • # coding:gbk
                • import sys

    import locale
                • def p(f):
    print '%s.%s(): %s' % (f.__module__, f.__name__, f())
                • # 返回当前系统所使用的默认字符编码
    p(sys.getdefaultencoding)
                • #
                • #重设编码
                        reload(sys)
                        sys.setdefaultencoding('gbk')
                        • 因为reload(sys)后，删除方法setdefaultencoding，需要我们重新载入。
        • 编码忠告：
                • 尽量都选择utf8 ,文件格式编码和声明编码统一。
        • 技巧：
                • 看到一些错误的编码用python来解码 看是什么编码
                        • 
    
    
为什么有效 
    
    import sys
    reload(sys)
    sys.setdefaultencoding("utf-8")
    作用:
        1.将decode默认的asc码变为了，utf8。其实这个功能可以通过unicode('','utf8')
        2.sys.stdout.encoding  置为utf8.

    这段代码的主要因为 sys.stdout.encoding 没有定义。所以在输出utf8编码的时候会报错。

    参考链接:
    http://stackoverflow.com/questions/3828723/why-we-need-sys-setdefaultencodingutf-8-in-a-py-script
    https://github.com/ajiexw/Ajiex.com/blob/master/%E8%A7%A3%E5%86%B3UnicodeDecodeError-%20'ascii'%20codec%20can't%20decode%20byte%200xe5%20in%20position%20108-%20ordinal%20not%20in%20range(128).md%20%20.md
## Python 的模块 ##
json
[json 中文乱码，ensure_ascii 问题 ](http://yangpengg.github.io/blog/2012/12/13/decode-and-encode-in-python/)


        json.dumps({"你还":2},encoding="utf-8",ensure_ascii=False) -- ensure_ascii=False输出中文
        json.dumps(rs,ensure_ascii=False,encoding="utf8").encode("utf8") -- 注意增加 encode('utf8') 

        因为出错是json打印出来ascii 不能解析，所以需要对结果

    • Python Modules 
    • Python hashlib md5 hash
        1.首先从python直接导入hashlib模块
        2.调用hashlib里的md5()生成一个md5 hash对象
        3.生成hash对象后，就可以用update方法对字符串进行md5加密的更新处理
        4.继续调用update方法会在前面加密的基础上更新加密
        5.加密后的二进制结果
        6.十六进制结果
        >>>print hashlib.new("md5", "Nobody inspects the spammish").hexdigest()
        'bb649c83dd1ea5c9d9dec9a18df0ffe9'
    • 随机函数
        Import  random
        random.random()() 生成0至1之间的随机浮点数，结果大于等于0.0，小于1.0
        random.randint(a,b) 生成1至5之间的随机整数，结果大于等于1，小于等于5，a必须小于等于b
        random.choice(testlist)从testlist中随机挑选一个数，也可以是元组、字符串
    • 本地化 locale
        ○ setlocale valueerror too many values to unpack 
            § 传unicode出问题，传str. 所以在setting 中设置 shopping_currency=b'en_US.UTF-8'
        ○ locale 的起源等。
    • functools
        ○ reduce
            § 和python 内置的一样。
#### itertools
[使用参考](http://powerelite.blog.163.com/blog/static/42965891201422731450746/) 
[进阶](http://www.wklken.me/posts/2013/08/20/python-extra-itertools.html)
#### python 时间

**模块 arrow**
    
    arrow.get("2015-04-24","YYYY-MM-DD")
    arrow.get("2015-04-24","YYYY-MM-DD").floor("day").timestamp
    arrow.get(1367900664)
    当天的起始时间 ：arw.now().floor('day').timestamp
    结束时间： arrow.now().ceil('hour')

**问题**
    
get 默认为utc时区，修改该时区。
    
    arrow.get(time, 'DD/MMM/YYYY:HH:mm:ss').replace(tzinfo='local').timestamp

### logging ### 

    关于字符串
        使用logging自带的arg。这样高level时，低level不会执行多余的字符串拼接。

### Collections ###

#### counter ####
**初始化**

    >>> c = Counter()                           # a new, empty counter
    >>> c = Counter('gallahad')                 # a new counter from an iterable
    >>> c = Counter({'red': 4, 'blue': 2})      # a new counter from a mapping
    >>> c = Counter(cats=4, dogs=8)             # a new counter from keyword args
    >>> c = Counter(['eggs', 'ham'])

**方法**
    
    elements()
        返回keys
    most_common([n])
        返回最近n个

#### OrderedDict ###

__记录记录的插入顺序__

可以作为程序的





## python 的迭代器、生成器、yield ##

#### 迭代器 iterator

`iterator`  是一种常见的设计模式在 Python 中恰好可以用 generator 这种 function 实现而已。iterator 有其他的实现方式，例如自己在类里定义__iter__ 和 next 方法。

        ○ where 
            § 用迭代器来读取内容，减少一次性的占用过大的内存。
            § 让文件、列表等都实现迭代器，方便统一访问。
            § 
        ○ what
            § 可以遍历的目标的迭代器对象
        ○ how:
            § 通过实现迭代器的协议，实现了next(),方法在文件最后跑出stopiterator exception, 来实现对文件、列表等元素的统一的访问。
    


#### 生成器 generator
关于send,next,yield,stopIteration

yield 返回generaotr
next  从过程上看，是执行了从开始到yield的部分
send 返回信息给yield
函数执行完 抛出stopIteration

`generator` 的定义是

    A function which returns an iterator. It looks like a normal function except that it contains yield statements for producing a series a values usable in a for-loop or that can be retrieved one at a time with the next() function.


        ○ 理解：http://www.cnblogs.com/tqsummer/archive/2010/12/27/1917927.html
        ○ where  包含yield的语句会被编译成生成器形式。
        ○ what 生成器
            i.  支持迭代器的接口
            ii. 不像return 是直接返回函数。生成器会将当前函数挂起
    一些比较有用的地方 
    Generators as a Pipeline
        wwwlog = open("access-log")
        bytecolumn = (line.rsplit(None,1)[1] for line in wwwlog)
        bytes = (int(x) for x in bytecolumn if x != '-')
        print "Total", sum(bytes)
    • yield
        ○ 链接
            § http://www.ibm.com/developerworks/cn/opensource/os-cn-python-yield/  通过费波浪旗来讲解的
            § http://www.jb51.net/article/15717.htm  深入的讲解了next(), send()，及中断generator的方法
        ○ where
            §  即实现了访问函数的当次返回值也实现了函数能够继续运行。
                □ for i in fab(20):
                    ® fab为构造费波浪旗数列
                    ® 那么每次运行都能够获取到该次的返回值的，同时，函数能正常运行。
        ○ what 用来返回函数当前值 且挂起当前函数的方法。用来循环的访问函数。
        ○ how
            § 关于next(),send()
                □ next()=send(None)
                □ send (msg)和next的含义就是传msg作为yield部分的传入参数（next传入的时none）让整改函数继续执行。
                □ 注意
                    ® 初始的时候不能用send往里面出入参数因为，就是第一次必须传none，我也不知道为啥。
                
        ○ use
            § 具体使用关于yield 的基本含义 和 next和send
            def h():
            ...     print 'dong jian'
            ...     m=yield 5
            ...     print str(m)+'hahahha'
            ...     d=yield 12
            ...     print 'we are together'
            c=h()
            >>> c.next()
            dong jian
            5
            >>> c.next()
            Nonehahahha
            12
            >>> c=h()
            >>> c.next()
            dong jian
            5
            >>> c.send('wo ai ni')
            wo ai nihahahha
            12
            
            
            § 实现费波浪旗数列
                def fab(max):
                a,b = 0,1
                while a < max:
                yield a
                a, b = b, a+b
                 
                >>> for i in fab(20):
                ...     print i,",",
                ...
                0 , 1 , 1 , 2 , 3 , 5 , 8 , 13 

    • (),[] 
        ○ () 返回值为生成器，可以使用next()方法
        ○ []返回值为list

    • 动态构建对象
        通过 
         test={}
        >>> for i in xrange(10):
        ...     test['a'+str(i)]=i
        ... 
        >>> print test
        {'a1': 1, 'a0': 0, 'a3': 3, 'a2': 2, 'a5': 5, 'a4': 4, 'a7': 7, 'a6': 6, 'a9': 9, 'a8': 8}
    
    • locals() 返回当前系统中的键值变量对
        ○ 比如{'HttpRequest': <class 'django.http.request.HttpRequest'>, 'foo': <function foo at 0x105e45668>, '__builtins__': <module '__builtin__' (built-in)>, 'l': [1, 2, 3], 'django': <module 'django' from '/Library/Python/2.7/site-packages/django/__init__.pyc'>, 'i': 9, 'test': {'a1': 1, 'a0': 0, 'a3': 3, 'a2': 2, 'a5': 5, 'a4': 4, 'a7': 7, 'a6': 6, 'a9': 9, 'a8': 8}, '__name__': '__main__', '__package__': None, '__doc__': None}
    • python 对象寻找方式
        ○ 局域变量
        ○ 全局
        ○ 内置变量
    • 实例变量 和类变量
        ○ 实例变量 是 运行时候定制的 在__init__中定义的。
        ○ 类变量是雷属性，直接写在类里的。
        
    • 静态方法和类方法
        ○ 静态方法是方法，但是属于类的作用域。
        ○ 类方法，不能访问实例变量但是可以访问类变量的值.
        静态方法：无法访问类属性、实例属性，相当于一个相对独立的方法，跟类其实没什么关系，换个角度来讲，其实就是放在一个类的作用域里的函数而已。
        类成员方法：可以访问类属性，无法访问实例属性。上述的变量val1，在类里是类变量，在实例中又是实例变量，所以容易混淆。
        
        ○ 参考
            § http://www.cnblogs.com/2gua/archive/2012/09/03/2668125.html
#### 列表解析、生成器表达式 

__效率对比__
    
    迭代器
    from time import time  
    t = time()
    list = ['a','b','is','python','jason','hello','hill','with','phone','test',
    'dfdf','apple','pddf','ind','basic','none','baecr','var','bana','dd','wrd']
    total=[]
    for i in range (1000000):
        for w in list:
            total.append(w)
    print "total run time:"
    print time()-t

    t= time()
    for i in range (1000000):
        a = [w for w in list]
    print "total runtime is {0}".format(time()-t)


    t= time()
    for i in range (1000000):
        a = (w for w in list)
    print "total runtime is {0}".format(time()-t)



# Python 文件操作 #
    os.path.exists('d:/assist/getTeacherList.py')
    • 获取python 模块的路径
        import moduel
        print module.__file__
    获取文件的上一级目录
        os.path.dir

        
    
    
    
    


# Python 高级#

## python 装饰器##
    例题:
    @test(a=2)
    def func():
        pass
    func = test(a=2)func()
    这里面是先处理参数。
    what：
        类似于切面编程，aop，可以在前后做很多事情。比如 引入日志、引入计时逻辑来检测性能、给函数增加事务的能力。
    how：
        def deco(func):
            print func
            return func 
            #这里是返回是func ，如果是有参数的装饰器，那么这时候应该在内部再加一层。
        @deco
        def foo():
            pass
        foo() #相当于是 deco(foo)
    use：
        ○ 装饰器无参数。
            好例子： 检查函数是否有文档。
                def deco_functionNeedDoc(func):  
                   ls if func.__doc__ == None : , 
                        print func, "has no __doc__, it's a bad habit."  
                    else:  
                        print func, ':', func.__doc__, '.'  
                    return func  
                @deco_functionNeedDoc  
                def f():  
                    print 'f() Do something'  
                
        ○ 有参数装饰器，被装饰函数无参数
            def deco(argv):
                def decorator(func):
                    print "decorator"
                    return func
                print "deco"
                print argv
                return decorator
            @deco("123")
            def foo():
                print “foo”
        ○ 有参数装饰器，被装饰函数有参数
            def deco(argv):  
                def decorator(func):  
                    @wraps(func)  
                    def wrapper(*args, **kwargs):  
                        print("wrapper")  
                        return func(*args, **kwargs)  
                    print("decorator")  
                    return wrapper  
                print("deco")  
                print(argv)  
                return decorator  
             
            @deco("123")  
            def foo(data):  
                "this is foo"  
                print("foo")  
                print(data)  
            § 相当于是 deco(argv)(foo)(data)
            § functools.wrapper 是讲返回的func的常用属性赋予给了，wrapper 函数，所以在wrapper返回里面依然是foo。
            § 实例
                □ 锁同步的装饰方法
                    1. def synchronized(lock):  
                    2.     """锁同步装饰方法 
                    3.     ！lock必须实现了acquire和release方法 
                    4.     """  
                    5.     def sync_with_lock(func):  
                    6.         def new_func(*args, **kwargs):  
                    7.             lock.acquire()  
                    8.             try:  
                    9.                 return func(*args, **kwargs)  
                    10.             finally:  
                    11.                 lock.release()  
                    12.         new_func.func_name = func.func_name  
                    13.         new_func.__doc__ = func.__doc__  
                    14.         return new_func  
                    15.     return sync_with_lock  
                    16. @synchronized(__locker)  
                    17. def update(data):  
                    18. """更新计划任务"""  
                    19.     tasks = self.get_tasks()  
                    20.     delete_task = None  
                    21.     for task in tasks:  
                    22.         if task[PLANTASK.ID] == data[PLANTASK.ID]:  
                    23.             tasks.insert(tasks.index(task), data)  
                    24.             tasks.remove(task)  
                    25.             delete_task = task  
                    26.     r, msg = self._refresh(tasks, delete_task)  
                    27.     return r, msg, data[PLANTASK.ID]  
                    
        ○ 多个装饰器
            § 从下至上。
                1. def makebold(func):  
                2.     def wrapped():  
                3.         return "<b>" + func() + "</b>"  
                4.     return wrapped  
                5.   
                6. def makeitalic(func):  
                7.     def wrapped():  
                8.         return "<i>" + func() + "</i>"  
                9.     return wrapped  
                10.  
                11. @makebold  
                12. @makeitalic  
                13. def say():  
                14.     return "Hello"  
                15.   
                16. print(say())  
                17. #output  
                18. ''''' 
                19. <b><i>Hello</i></b> 
              
            
        ○ 装饰类
            § 装饰器接收一个函数，并返回一个函数，从而起到加工函数的效果。在Python 2.6以后，装饰器被拓展到类。一个装饰器可以接收一个类，并返回一个类，从而起到加工类的效果。
            def decorator(aClass):
    class newClass:
        def __init__(self, age):
            self.total_display   = 0
            self.wrapped         = aClass(age)
        def display(self):
            self.total_display += 1
            print("total display", self.total_display)
            self.wrapped.display()
    return newClass
            @decorator
    class Bird:
        def __init__(self, age):
            self.age = age
        def display(self):
            print("My age is",self.age)
                eagleLord = Bird(5)
    for i in range(3):
        eagleLord.display()
            
            § 在decorator中，我们返回了一个新类newClass。在新类中，我们记录了原来类生成的对象（self.wrapped），并附加了新的属性total_display，用于记录调用display的次数。我们也同时更改了display方法。通过修改，我们的Bird类可以显示调用display的次数了。
    
    
    
##  contextmanager 

    @contextmanager
    def myfile(name):
        f=open(name)
        try:
            yield f
        finally:
            print 'finally'
            f.close()

    with myfile('test.py') as f:
        for x in f:
            print x
    

## lru
使用装饰器来构造初始化的lru

    def go(start= False):

    @lru_cache_function()
    def lru(a):
        print "not in cache",a
        return a+1

    [lru(x) for x in range(5)]
    return lru



    """
    2015-06-12: copy from https://github.com/stucchio/Python-LRU-cache
    """

    from collections import OrderedDict
    import time
    from itertools import islice
    import threading
    import weakref
    from contextlib import contextmanager

    def lru_cache_function(max_size=1024, expiration=15*60):
        """
        >>> @lru_cache_function(3, 1)
        ... def f(x):
        ...    print "Calling f(" + str(x) + ")"
        ...    return x
        >>> f(3)
        Calling f(3)
        3
        >>> f(3)
        3
        """
        def wrapper(func):
            return LRUCachedFunction(func, LRUCacheDict(max_size, expiration))
        return wrapper

    def _lock_decorator(func):
        """
        If the LRUCacheDict is concurrent, then we should lock in order to avoid
        conflicts with threading, or the ThreadTrigger.
        """
        def withlock(self, *args, **kwargs):
            if self.concurrent:
                with self._rlock:
                    return func(self, *args, **kwargs)
            else:
                return func(self, *args, **kwargs)
        withlock.__name__ == func.__name__
        return withlock

    class LRUCacheDict(object):
        """ A dictionary-like object, supporting LRU caching semantics.
        >>> d = LRUCacheDict(max_size=3, expiration=3)
        >>> d['foo'] = 'bar'
        >>> d['foo']
        'bar'
        >>> import time
        >>> time.sleep(4) # 4 seconds > 3 second cache expiry of d
        >>> d['foo']
        Traceback (most recent call last):
            ...
        KeyError: 'foo'
        >>> d['a'] = 'A'
        >>> d['b'] = 'B'
        >>> d['c'] = 'C'
        >>> d['d'] = 'D'
        >>> d['a'] # Should return value error, since we exceeded the max cache size
        Traceback (most recent call last):
            ...
        KeyError: 'a'
        By default, this cache will only expire items whenever you poke it - all methods on
        this class will result in a cleanup. If the thread_clear option is specified, a background
        thread will clean it up every thread_clear_min_check seconds.
        If this class must be used in a multithreaded environment, the option concurrent should be
        set to true. Note that the cache will always be concurrent if a background cleanup thread
        is used.
        """
        def __init__(self, max_size=1024, expiration=15*60, thread_clear=False, thread_clear_min_check=60, concurrent=False):
            self.max_size = max_size
            self.expiration = expiration

            self.__values = {}
            self.__expire_times = OrderedDict()
            self.__access_times = OrderedDict()
            self.thread_clear = thread_clear
            self.concurrent = concurrent or thread_clear
            if self.concurrent:
                self._rlock = threading.RLock()
            if thread_clear:
                t = self.EmptyCacheThread(self)
                t.start()

        class EmptyCacheThread(threading.Thread):
            daemon = True

            def __init__(self, cache, peek_duration=60):
                me = self
                def kill_self(o):
                    me
                self.ref = weakref.ref(cache)
                self.peek_duration = peek_duration
                super(LRUCacheDict.EmptyCacheThread, self).__init__()

            def run(self):
                while self.ref():
                    c = self.ref()
                    if c:
                        next_expire = c.cleanup()
                        if (next_expire is None):
                            time.sleep(self.peek_duration)
                        else:
                            time.sleep(next_expire+1)
                    c = None

        @_lock_decorator
        def size(self):
            return len(self.__values)

        @_lock_decorator
        def clear(self):
            """
            Clears the dict.
            >>> d = LRUCacheDict(max_size=3, expiration=1)
            >>> d['foo'] = 'bar'
            >>> d['foo']
            'bar'
            >>> d.clear()
            >>> d['foo']
            Traceback (most recent call last):
            ...
            KeyError: 'foo'
            """
            self.__values.clear()
            self.__expire_times.clear()
            self.__access_times.clear()

        def __contains__(self, key):
            return self.has_key(key)
            
        @_lock_decorator
        def has_key(self, key):
            """
            This method should almost NEVER be used. The reason is that between the time
            has_key is called, and the key is accessed, the key might vanish.
            You should ALWAYS use a try: ... except KeyError: ... block.
            >>> d = LRUCacheDict(max_size=3, expiration=1)
            >>> d['foo'] = 'bar'
            >>> d['foo']
            'bar'
            >>> import time
            >>> if d.has_key('foo'):
            ...    time.sleep(2) #Oops, the key 'foo' is gone!
            ...    d['foo']
            Traceback (most recent call last):
            ...
            KeyError: 'foo'
            """
            return key in self.__values

        @_lock_decorator
        def __setitem__(self, key, value):
            t = int(time.time())
            self.__delete__(key)
            self.__values[key] = value
            self.__access_times[key] = t
            self.__expire_times[key] = t + self.expiration
            self.cleanup()

        @_lock_decorator
        def __getitem__(self, key):
            t = int(time.time())
            del self.__access_times[key]
            self.__access_times[key] = t
            self.cleanup()
            return self.__values[key] if self.has_key(key) else None

        @_lock_decorator
        def __delete__(self, key):
            if key in self.__values:
                del self.__values[key]
                del self.__expire_times[key]
                del self.__access_times[key]

        @_lock_decorator
        def cleanup(self):
            if self.expiration is None:
                return None
            t = int(time.time())
            #Delete expired
            next_expire = None
            for k in self.__expire_times:
                if self.__expire_times[k] < t:
                    self.__delete__(k)
                else:
                    next_expire = self.__expire_times[k]
                    break

            #If we have more than self.max_size items, delete the oldest
            while (len(self.__values) > self.max_size):
                for k in self.__access_times:
                    self.__delete__(k)
                    break
            if not (next_expire is None):
                return next_expire - t
            else:
                return None

    class LRUCachedFunction(object):
        """
        A memoized function, backed by an LRU cache.
        >>> def f(x):
        ...    print "Calling f(" + str(x) + ")"
        ...    return x
        >>> f = LRUCachedFunction(f, LRUCacheDict(max_size=3, expiration=3) )
        >>> f(3)
        Calling f(3)
        3
        >>> f(3)
        3
        >>> import time
        >>> time.sleep(4) #Cache should now be empty, since expiration time is 3.
        >>> f(3)
        Calling f(3)
        3
        >>> f(4)
        Calling f(4)
        4
        >>> f(5)
        Calling f(5)
        5
        >>> f(3) #Still in cache, so no print statement. At this point, 4 is the least recently used.
        3
        >>> f(6)
        Calling f(6)
        6
        >>> f(4) #No longer in cache - 4 is the least recently used, and there are at least 3 others items in cache [3,4,5,6].
        Calling f(4)
        4
        """
        def __init__(self, function, cache=None):
            if cache:
                self.cache = cache
            else:
                self.cache = LRUCacheDict()
            self.function = function
            self.__name__ = self.function.__name__

        def __call__(self, *args, **kwargs):
            key = repr( (args, kwargs) ) + "#" + self.__name__ #In principle a python repr(...) should not return any # characters.
            try:
                return self.cache[key]
            except KeyError:
                value = self.function(*args, **kwargs)
                self.cache[key] = value
                return value
    def go(start= False):

        @lru_cache_function()
        def lru(a):
            print "not in cache",a
            return a+1

        [lru(x) for x in range(5)]
        return lru

    if __name__ == "__main__":
        lru = go()

        print lru(1)
        print lru(1)
        # import doctest
        # doctest.testmod()


## python 动态加载##
    • __import__ 可以在程序中动态加载模块。而不是在程序开始加载。
        ○ _temp = __import__('spam.ham', globals(), locals(), ['eggs', 'sausage'], -1) 
            § 从spam.ham 导入eggs和sausage
## python 深拷贝 浅拷贝##
    • python 复制对象的时候都是传值，当需要拷贝对象的时候，需要使用库函数，copy.copy ()浅拷贝和copy.deepcopy() 深拷贝。   
        ○ 这里的例子。
        1. copy.copy 浅拷贝 只拷贝父对象，不会拷贝对象的内部的子对象。
        2. copy.deepcopy 深拷贝 拷贝对象及其子对象
        一个很好的例子：
        import copy
        a = [1, 2, 3, 4, ['a', 'b']]  #原始对象
        b = a  #赋值，传对象的引用
        c = copy.copy(a)  #对象拷贝，浅拷贝
        d = copy.deepcopy(a)  #对象拷贝，深拷贝
        a.append(5)  #修改对象a
        a[4].append('c')  #修改对象a中的['a', 'b']数组对象
        
        print 'a = ', a
        
        print 'b = ', b
        
        print 'c = ', c
        
        print 'd = ', d
        输出结果：
        a =  [1, 2, 3, 4, ['a', 'b', 'c'], 5]
        b =  [1, 2, 3, 4, ['a', 'b', 'c'], 5]
        c =  [1, 2, 3, 4, ['a', 'b', 'c']]
        d =  [1, 2, 3, 4, ['a', 'b']]
        
        关于复制自定义对象：
        class Node:
                val=1
                left=None
                right=None
        
        复制对象是一样的。但是这里有个问题，什么问题呢？ 就是left这个属性如果赋值的是，这里如果是对象，注意是对象，不是包含自带对象的对象 比如 Node 和 [Node] 如果是前者 将会被复制，后者则需要deepcopy
## Python setup.py install/develop##
    • Install :
        ○ 安装第三方包。一般用于第三方包，如果更改需要重新安装才能生效。 
    • Develop ：
        ○ 安装自己的包。更改立刻生效，通过建立当前项目到site-package的链接来实现。
        ○ 1.在指定的地方安装包 2. 建立链接到site-packages
    • 也理解了为什么在cartridge 当中需要python setup.py develop。
    
## Python 的类 ##

    • 实例化的代码
        ○  a=ClassA(agr1,arg2)相当于 调用了类的call。实例化就是调用了call方法。
            § a = type(ClassA).__call__(ClassA,arg1,arg2)
                Def __call__(cls,*args,**args):
                        Result=cls.__new__(cls,*args,**kwargs)
                        If isinstance(result,cls):
                                Type(result).__init__(result,*args,**kwargs)
                        Return result
                

    Python 中的self,cls:
        二者都代表自身。但是其实都是约定的写法。不距有实际意义。

    Python 中的oject,__init__ , __new__
        为什么继承object ？
            继承object 生成的类型为 type  'type' 。这样的好处是可以使用一些新的特性 比如 metaclass
        顺序 __new__, __init___
        Where
            __init__ 用来将传入的参数初始化的
            __new__ 用来控制对象的创建
    类的__call__
    object.__call__(self[, args...])

###     关于classmethod staticmethod
定义
    
    Convert a function to be a class method.
    
    A class method receives the class as implicit first argument,
    just like an instance method receives the instance.
    To declare a class method, use this idiom:


自己试验
    
    class ccc(object):
        @classmethod
        def nihao(self):
            print "nihao"


    ccc().nihao()
    ccc.nihao()

    不加上，classmethod 不能用类来调用。

类方法常用于构造类实例。

    class MyStream(object):

    @classmethod
    def from_file(cls, filepath, ignore_comments=False):    
        with open(filepath, 'r') as fileobj:
            for obj in cls(fileobj, ignore_comments):
                yield obj

    @classmethod
    def from_socket(cls, socket, ignore_comments=False):
        raise NotImplemented # Placeholder until implemented

    def __init__(self, iterable, ignore_comments=False):

[一个贯穿classmethod ，static method 用法的网页。](http://stackoverflow.com/questions/12179271/python-classmethod-and-staticmethod-for-beginner?rq=1)

    Though classmethod and staticmethod are quite similar, there's a slight difference in usage for both entities: classmethod must have a reference to a class object as the first parameter, whereas staticmethod can have no parameters at all.

    Let's look at all that was said in real examples.

    Boilerplate

    Let's assume an example of a class, dealing with date information (this is what will be our boilerplate to cook on):

    class Date(object):

        day = 0
        month = 0
        year = 0

        def __init__(self, day=0, month=0, year=0):
            self.day = day
            self.month = month
            self.year = year
    This class obviously could be used to store information about certain dates (without timezone information; let's assume all dates are presented in UTC).

    Here we have __init__, a typical initializer of Python class instances, which receives arguments as a typical instancemethod, having the first non-optional argument (self) that holds reference to a newly created instance.

    Class Method

    We have some tasks that can be nicely done using classmethods.

    Let's assume that we want to create a lot of Date class instances having date information coming from outer source encoded as a string of next format ('dd-mm-yyyy'). We have to do that in different places of our source code in project.

    So what we must do here is:

    Parse a string to receive day, month and year as three integer variables or a 3-item tuple consisting of that variable.
    Instantiate Date by passing those values to initialization call.
    This will look like:

    day, month, year = map(int, string_date.split('-'))
    date1 = Date(day, month, year)
    For this purpose, C++ has such feature as overloading, but Python lacks that feature- so here's when classmethod applies. Lets create another "constructor".

        @classmethod
        def from_string(cls, date_as_string):
            day, month, year = map(int, date_as_string.split('-'))
            date1 = cls(day, month, year)
            return date1

    date2 = Date.from_string('11-09-2012')
    Let's look more carefully at the above implementation, and review what advantages we have here:

    We've implemented date string parsing in one place and it's reusable now.
    Encapsulation works fine here (if you think that you could implement string parsing as a single function elsewhere, this solution fits OOP paradigm far better).
    cls is an object that holds class itself, not an instance of the class. It's pretty cool because if we inherit our Date class, all children will have from_string defined also.
    Static method

    What about staticmethod? It's pretty similar to classmethod but doesn't take any obligatory parameters (like a class method or instance method does).

    Let's look at the next use case.

    We have a date string that we want to validate somehow. This task is also logically bound to Date class we've used so far, but still doesn't require instantiation of it.

    Here is where staticmethod can be useful. Let's look at the next piece of code:

        @staticmethod
        def is_date_valid(date_as_string):
            day, month, year = map(int, date_as_string.split('-'))
            return day <= 31 and month <= 12 and year <= 3999

        # usage:
        is_date = Date.is_date_valid('11-09-2012')
    So, as we can see from usage of staticmethod, we don't have any access to what the class is- it's basically just a function, called syntactically like a method, but without access to the object and it's internals (fields and another methods), while classmethod does.



## metaclass 元类 ##

    What
        定义:metaclass 的实例是类(metaclass 可以理解成类的模板，)。而class 的实例结果是instance。
        
        作用:
            § 自由的、动态的修改/增加/删除类的实例中的方法或者属性。
            § 批量的对某些方法是用装饰器，不用每次都在方法的上面加入@decorater_func
            § 第三库需要patch的时候，可以用metaclass
            § 用于序列化(yaml)
            § 接口注册，接口格式审查等。
            § 自动委托(auto delegate)
            § more...
    参考:
        http://jianpx.iteye.com/blog/908121
        
        http://blog.jobbole.com/21351/2
    How
        a. 拦截类的创建（a=classA(a) , -- 并没有一开始就在内存中创建类 ，而是先去找metaclass。）
        b. 修改类
        c. 返回类
            -- exp：将类的属性都变成大写。
        
    Where
        ○ 主要用来整合比较复杂的函数？？？
        ○ 主要用来是创建API
            § 如
                class Person(models.Model):
                    name = models.CharField(max_length=30)
                    age = models.IntegerField()
                guy  = Person(name='bob', age='35')
                print guy.age
                
                这段代码 guy.age  返回的是一个int 对象，而不是一个integerfield。这里person类集成的models.Model中就是一个定义了metaclass 执行了如数据库抽取，类型转换等操作。
        ○ ？分布式 ruby
        ○ ？反省
            § 参考松本猩红的程序世界
    use
        定义模板级别的元类  -- 使用元类来让类的属性都变大写 -- 可运行
        
            def upper_attr(future_class_name,future_class_parents,future_class_attr):
                attrs=((name,value) for name,value in future_class_attr.items() if not name.startswith('__'))
                uppercase_attr=dict((name.upper(),value) for name,value in attrs)
                return type(future_class_name,future_class_parents,uppercase_attr)
        
            __metaclass__= upper_attr
            
            class Foo():
                bar='bip'
        
    关于类的本质的说明
        >>> class Bar(object):pass
        ... 
        >>> b=Bar()   
        >>> print b.__class__
        <class '__main__.Bar'>
        >>> print Bar.__class__ -- 打印类的源类
        <type 'type'>
        >>> print Bar  -- 打印类 
        <class '__main__.Bar'> 
        >>> print b -- 打印对象 为object
        <__main__.Bar object at 0x10da58150>
        >>> print b.__class__
        <class '__main__.Bar'>
    参考
        http://blog.jobbole.com/21351/
        
## 鸭子类型 、多肽##
    Where 
        鸭子类型是从哪来的？
            我想主要是用来让语言更灵活，忽略类型。
                比如 +，* 等。 可以是 1+1 也可以是 'a'+'a' 这种写法就是忽略了类型。只要能加就可以加。
        思想
            忽略类型，重视方法，只要实现了方法，就可以执行。
            
    What
        当看到一只鸟走起来像鸭子、游泳起来像鸭子、叫起来也像鸭子，那么这只鸟就可以被称为鸭子。
    USE
        说明 这里john 也可以使用in_the_forest方法。因为他有quack和feather方法，即为有方法即可执行。
        class Duck:
            def quack(self): 
                print "Quaaaaaack!"
            def feathers(self): 
                print "The duck has white and gray feathers."
         
        class Person:
            def quack(self):
                print "The person imitates a duck."
            def feathers(self): 
                print "The person takes a feather from the ground and shows it."
         
        def in_the_forest(duck):
            duck.quack()
            duck.feathers()
         
        def game():
            donald = Duck()
            john = Person()
            in_the_forest(donald)
            in_the_forest(john)
         
        game()
        
    Further use 
    
## python 回调函数## 
    • what
        § 函数完成之后，调用的函数 叫做回调
    

        

闭包
    
    http://tc.uc.cn/?src=http%3A%2F%2Fm.baidu.com%2Ffrom%3D2001a%2Fbd_page_type%3D1%2Fssid%3D0%2Fuid%3D0%2Fpu%3Dusm%25400%252Csz%25401320_1003%252Cta%2540iphone_2_4.4_1_9.8%2Fbaiduid%3D6C1C3ED0B2883445AE6E7591B4585E25%2Fw%3D0_10_python%2B%25E9%2597%25AD%25E5%258C%2585%2Ft%3Diphone%2Fl%3D3%2Ftc%3Fref%3Dwww_iphone%26lid%3D9328264885350547270%26order%3D1%26vit%3Dosres%26tj%3Dwww_normal_1_0_10%26m%3D8%26srd%3D1%26cltj%3Dcloud_title%26dict%3D30%26sec%3D39136%26di%3D22ebe3d755916e12%26bdenc%3D1%26nsrc%3DIlPT2AEptyoA_yixCFOxXnANedT62v3IJBaOMmBXATq5953ybrWxBdlbUCPmX87DZpPPxXCKe1xRdWGdWTJznMESgO66sVsc8XbkdfXv&restype=1&ucshare=1&ucshareplatform=-1&country=cn
    
    what
        >>> def F(name):
            def f():
                print name
            return f
         
        >>> f1=F('f1')
        >>> f2=F('f2')
        >>> f1()
        f1
        >>> f2()
        f2
        F 是一个返回函数的函数。对于 F 产生的函数 f1、f2，其依赖于F的本地变量 name，但是在F执行结束后，函数 f1、f2 依然可以访问 name，而且相互独立。就像在返回内层函数时，把产生它的环境一块儿打包返回了，这种语法现象叫闭包（closure）。
        1   >>> def gen_ins(init):
        2       i=init-1
        3       def ins():
        4           i=i+1
        5           return i
        6       return ins
        7    
        8   >>> ins0=gen_ins(0)
        9   >>> ins0()
        10   
        11  Traceback (most recent call last):
        12    File "<pyshell#111>", line 1, in <module>
        13      ins0()
        14    File "<pyshell#108>", line 4, in ins
        15      i=i+1
        16  UnboundLocalError: local variable 'i' referenced before assignment
        python
        这就是所谓的 python 不支持真闭包，python 中对外层变量不能赋值。一般在 python 的函数中，变量的查找顺序是局部符号表，全局符号表，内置符号表。我们知道，全局变量可以被引用，但是要赋值的话，必须用 global 声明一下，否则其实是新建了一个本地变量。从python解释器的角度看，“i=i+1”中 i 既然被赋值，就应该当做本地变量，所以就会发生上述 UnboundLocalError 错误。i 也并不是全局变量，所以在 ins 中用 global 声明了 i 则会找不到全局变量。按照 PEP3104 来看，这是一个由来已久的问题。
        
    where 
        a. 闭包执行完后，仍能保持当前的执行环境。
    
    以上两种使用场景，用面向对象也是可以很简单的实现的，但是在用Python进行函数式编程时，闭包对数据的持久化以及按配置产生不同的功能，是很有帮助的。
    what 函数快+ 函数的环境
        1. >>>def addx(x):  
        2. >>>    def adder(y): return x + y  
        3. >>>    return adder  
        4. >>> c =  addx(8)  
        5. >>> type(c)  
        6. <type 'function'>  
        7. >>> c.__name__  
        8. 'adder'  
        9. >>> c(10)  
        10. 18  
        
        如果在一个内部函数里：adder(y)就是这个内部函数，
        对在外部作用域（但不是在全局作用域）的变量进行引用：x就是被引用的变量，x在外部作用域addx里面，但不在全局作用域里，
        则这个内部函数adder就是一个闭包。
        
    use
        a.     闭包执行完后，仍能保持当前的执行环境。
        用途1，当闭包执行完后，仍然能够保持住当前的运行环境。
        比如说，如果你希望函数的每次执行结果，都是基于这个函数上次的运行结果。我以一个类似棋盘游戏的例子来说明。假设棋盘大小为50*50，左上角为坐标系原点(0,0)，我需要一个函数，接收2个参数，分别为方向(direction)，步长(step)，该函1数控制棋子的运动。棋子运动的新的坐标除了依赖于方向和步长以外，当然还要根据原来所处的坐标点，用闭包就可以保持住这个棋子原来所处的坐标。
        1. origin = [0, 0]  # 坐标系统原点  
        2. legal_x = [0, 50]  # x轴方向的合法坐标  
        3. legal_y = [0, 50]  # y轴方向的合法坐标  
        4. def create(pos=origin):  
        5.     def player(direction,step):  
        6.         # 这里应该首先判断参数direction,step的合法性，比如direction不能斜着走，step不能为负等  
        7.         # 然后还要对新生成的x，y坐标的合法性进行判断处理，这里主要是想介绍闭包，就不详细写了。  
        8.         new_x = pos[0] + direction[0]*step  
        9.         new_y = pos[1] + direction[1]*step  
        10.         pos[0] = new_x  
        11.         pos[1] = new_y  
        12.         #注意！此处不能写成 pos = [new_x, new_y]，原因在上文有说过  
        13.         return pos  
        14.     return player  
        15.   
        16. player = create()  # 创建棋子player，起点为原点  
        17. print player([1,0],10)  # 向x轴正方向移动10步  
        18. print player([0,1],20)  # 向y轴正方向移动20步  
        19. print player([-1,0],10)  # 向x轴负方向移动10步
        输出为
        20. [10, 0]  
        21. [10, 20]  
        22. [0, 20]  
    
        用途2，闭包可以根据外部作用域的局部变量来得到不同的结果，这有点像一种类似配置功能的作用，我们可以修改外部的变量，闭包根据这个变量展现出不同的功能。比如有时我们需要对某些文件的特殊行进行分析，先要提取出这些特殊行。
        [python] 
        1. def make_filter(keep):  
        2.     def the_filter(file_name):  
        3.         file = open(file_name)  
        4.         lines = file.readlines()  
        5.         file.close()  
        6.         filter_doc = [i for i in lines if keep in i]  
        7.         return filter_doc  
        8.     return the_filter  
        如果我们需要取得文件"result.txt"中含有"pass"关键字的行，则可以这样使用例子程序
        9. filter = make_filter("pass")  
        10. filter_result = filter("result.txt")  
        
        ○ 注意事项：
            § 不能修改外部作用域的局部变量
                >>> def foo():  
                ...     m = 0  
                ...     def foo1():  
                ...         m = 1  
                ...         print m  
                ...  
                ...     print m  
                ...     foo1()  
                ...     print m  

Python 多线程的锁

## Python 内存管理机制##
    • python 内存管理机制
        ○ 垃圾回收
            § 引用计数
                □ 原理：当一个对象的引用被创建或者复制时，对象的引用计数加1；当一个对象的引用被销毁时，对象的引用计数减1；当对象的引用计数减少为0时，就意味着对象已经没有被任何人使用了，可以将其所占用的内存释放了。
    虽然引用计数必须在每次分配和释放内存的时候加入管理引用计数的动作，然而与其他主流的垃圾收集技术相比，引用计数有一个最大的有点，即“实时性”，任何内存，一旦没有指向它的引用，就会立即被回收。而其他的垃圾收集计数必须在某种特殊条件下（比如内存分配失败）才能进行无效内存的回收。
    引用计数机制执行效率问题：引用计数机制所带来的维护引用计数的额外操作与Python运行中所进行的内存分配和释放，引用赋值的次数是成正比的。而这点相比其他主流的垃圾回收机制，比如“标记-清除”，“停止-复制”，是一个弱点，因为这些技术所带来的额外操作基本上只是与待回收的内存数量有关。
    如果说执行效率还仅仅是引用计数机制的一个软肋的话，那么很不幸，引用计数机制还存在着一个致命的弱点，正是由于这个弱点，使得侠义的垃圾收集从来没有将引用计数包含在内，能引发出这个致命的弱点就是循环引用（也称交叉引用）。
    问题：
    循环引用可以使一组对象的引用计数不为0，然而这些对象实际上并没有被任何外部对象所引用，它们之间只是相互引用。这意味着不会再有人使用这组对象，应该回收这组对象所占用的内存空间，然后由于相互引用的存在，每一个对象的引用计数都不为0，因此这些对象所占用的内存永远不会被释放。比如：
    a = []
    b = []
    a.append(b)
    b.append(a)
    print a
    [[[…]]]
    print b
    [[[…]]]
    这一点是致命的，这与手动进行内存管理所产生的内存泄露毫无区别。
    要解决这个问题，Python引入了其他的垃圾收集机制来弥补引用计数的缺陷：“标记-清除”，“分代回收”两种收集技术。
            § 标记清除
                □ 怎么解决的循环引用？
                    ® 这里的经典的例子是
    a=[]
    b=[]
    a.append(b)
    b.append(a)
    如果是引用计数则会发生二者死锁的问题。但是采用标记清楚则不会。
    因为删除a, 那么b就成了一个孤立的点，则一定会被标记 清楚算法清除掉。
                □ 原理
                    ® 原理：“标记-清除”采用了更好的做法，我们并不改动真实的引用计数，而是将集合中对象的引用计数复制一份副本，改动该对象引用的副本。对于副本做任何的改动，都不会影响到对象生命走起的维护。
    这个计数副本的唯一作用是寻找root object集合（该集合中的对象是不能被回收的）。当成功寻找到root object集合之后，首先将现在的内存链表一分为二，一条链表中维护root object集合，成为root链表，而另外一条链表中维护剩下的对象，成为unreachable链表。之所以要剖成两个链表，是基于这样的一种考虑：现在的unreachable可能存在被root链表中的对象，直接或间接引用的对象，这些对象是不能被回收的，一旦在标记的过程中，发现这样的对象，就将其从unreachable链表中移到root链表中；当完成标记后，unreachable链表中剩下的所有对象就是名副其实的垃圾对象了，接下来的垃圾回收只需限制在unreachable链表中即可。
            § 标记-清除压缩收集器
                □ 压缩方法把活动的对象越过空闲区滑动到堆的一端，在这个过程中，堆的另一端出现一个大的连续空闲区。所有被移动的对象的引用也被更新，指向新的位置。
          更新被移动的对象的引用有时候通过一个间接对象引用层可以变得更简单。不直接引用堆中的对象，对象的引用实际上指向一个对象句柄表。对象句柄才指向堆中对象的实际位置。当对象被移动了，只有这个句柄需要被更新为新位置。所有的程序中对这个对象的引用仍然指向这个具有新值的句柄，而句柄本身没有移动。这种方法简化了消除堆碎块的工作，但是每一次对象访问都带来了性能损失。
            § 拷贝算法
                □ 复制算法
    为了解决效率问题，一种称为复制（Copying）的收集算法就出现了，它将可用内存按容量划分为大小相等的两块，每次只是用其中一块。当这一块的内存用完了，就将还存活着的对象复制到另外一块上面，然后再把已使用过的内存空间一次清理掉。这样使得每次都是对其中的一块进行内存回收，没存分配时也就不用考虑内存碎片等复杂情况，只要移动堆顶指针，按顺序分配内存即可，实现简单，运行高效。只是这种算法的代价是将员村缩小为原来的一半，未免太高了一点。
    同样一幅图来说明回收算法在回收前后的内存变化。
     
     
    现在的商业虚拟机都采用这种收集算法来回收新生代，IBM的专门研究表明，新生代中的对象98%是朝生夕死的，所以并不需要按照1：1的比例来划分内存空间，而是将内存分为一块较大的Eden空间和两块较小的Survivor空间，每次使用Eden和其中的一块Survivor。当回收时，将Eden和Survivor中还存活着的兑现个一次性地拷贝到另外一块Survivor空间上，最后清理掉Eden和刚才用过的Survivor的空间。HotSpot虚拟机默认Eden和Survivor的大小比例是8：1，也就是每次新生代中可用内存空间为整个新生代容量的90%，只有10%的内存是会被浪费的。
            § 按代收集器
                □ 简单的停止并拷贝收集器的缺点是每一次收集时，所有的活动对象都必须被拷贝。大部分语言的大多数程序都有以下特点，如果我们全面考虑这些，拷贝算法的这个缺点足可以被改进的。
          (1) 大多数程序创建的大部分对象都具有很短的生命期。
          (2)大多数程序都创建一些具有非常长生命周期的对象。 
          简单的拷贝收集器浪费效率的一个上要原因就是、它们每次都把这些生命周期很长的对象来回拷贝，消耗大量时间。   
          按代收集的收集器通过把对象按照寿命来分组解决这个效率低下的问题，更多地收集那些短暂出现的年幼对象，而非寿命较长的对象。在这种方法里，堆被划分成两个或者更多的子堆，
    每一个子堆为一“代”对象服务。最年幼的那一代进行最频繁的垃圾收集。因为大多数对象都是短促出现的，只有很小部分的年幼对象可以在它们经历第一次收集后还存活。如果一个最年幼的对象经历了好几次垃圾收集后仍然存活，那么这个对象就成长为寿命更高的一代：它被转移到另外一个子堆中去。年龄更高的每一代的收集都没有年径的那一代来得频繁。每当对象在它所属的年龄层(代)中变得成熟(逃过了多次垃圾收集)之后，它们就被转移到更高的年龄层中去。 
          按代进行的收集技术除了可以应用于拷贝算法，也可以应用于标记并清除算法。不管在哪种情况下，把堆按照对象年龄层分解都可以提高最基本的垃级收集算法的性能。

## python 日志 ##

python timerotatingfilehandle 

    def init_logging(log_path):
        logging.basicConfig(level=logging.INFO,
                            format='%(asctime)s %(name)-12s %(levelname)-8s %(message)s')
        file_handler = TimedRotatingFileHandler(log_path + "/http_sniffer.log", when='midnight', backupCount=30)
        file_handler.setLevel(logging.INFO)
        formatter = logging.Formatter('%(asctime)s %(name)-12s %(levelname)-8s %(message)s')
        file_handler.setFormatter(formatter)
        logging.getLogger('').addHandler(file_handler)



## PYTHON 相关命令 ##
PIP 
    基本：pip install
    查看当前安装 pip freeze pip list （两者应该有区别就是不知道） 
    
    pip 安装
        § 先升级Python,执行
                2   wget http://www.python.org/ftp/python/2.7.5/Python-2.7.5.tgz
                3   tar zxvf Python-2.7.5.tgz
                4   cd Python-2.7.5
                5   ./configure (./configure --enable-unicode=ucs4 这样undefined symbol: PyUnicodeUCS2_Decode 的错误ll)
                6   make all
                7   make install
                8   make clean
                    make distclean
                    
                    /usr/local/bin/python2.7 -V 
                    然后查下当前的版本
                    python -V
                    我这里显示的是2.6.6
                    mv /usr/bin/python /usr/bin/python2.6.6 --备份
                    ln -s /usr/local/bin/python2.7 /usr/bin/python
                    链接库等 --这一步我有时候把后面的改为/usr/local/bin/python 才好使
                    
                    修改yum不能使用问题
                    vi /usr/bin/yum
                    #!/usr/bin/python --》 #!/usr/bin/python2.6
                    
                    
                    pip 安装
                    
                    先安装setup-tools
                    wget https://pypi.python.org/packages/2.7/s/setuptools/setuptools-0.6c11-py2.7.egg  --no-check-certificate
    chmod +x setuptools-0.6c11-py2.7.egg
    sh setuptools-0.6c11-py2.7.egg
                        安装pip
                        wget https://pypi.python.org/packages/source/p/pip/pip-1.3.1.tar.gz --no-check-certificate
    cp pip-1.3.1.tar.gz /usr/src/
    tar zxvf pip-1.3.1.tar.gz
    cd pip-1.3.1
    python setup.py install
                        ln -s /usr/local/python2.7/bin/pip /usr/bin/pip
                    
                    --- pip 不好使的时候 直接使用easy_install 升级
                    
                    
                    --------------------
                    降级python 2.6
                    wget https://www.python.org/ftp/python/2.6.6/Python-2.6.6.tgz
                    wget https://www.python.org/ftp/python/2.5.5/Python-2.5.5.tgz
    ○ http://www.love4026.org/313724/centos-6-4下的python2-6-6下安装pip/
    
    pip 技巧
        pip install -r requirements.txt 
        pip freeze 
        env1/bin/pip freeze > requirements.txt
    $ env2/bin/pip install -r requirements.txt
        trouble shooting 
            问题：使用virtualenv的时候不管怎样，pip使用的都是lib下的
            答案:那么删除bin文件夹，重新建立。 往往是因为之前的错误建立导致的。

## python 效率note ##
    
关于python的[性能分析](http://www.huyng.com/posts/python-performance-analysis/)

memory profile 

line profile 
    
    安装
    pip install line-prolfer

    使用

    python "C:\Python27\Scripts\kernprof.py" -l -v example.py

[profile 参考](http://stackoverflow.com/questions/582336/how-can-you-profile-a-python-script)
### 关于对象大小 ###

同样内容，dict的存储是list的接近10倍。

list的extend 是+ 的10呗效率
    
    why 

Counter的


# python 小问题 

**python转移字符**

    escape_comma = lambda x: x.replace(',',str(hex(ord(','))))

# python 学习



##  pandas

# python 协程

携程 其实并不是并行。只是在遇到阻塞的时候，显示的切换到其他地方运行。 通过栈和堆的切换来实现。

    一个 “greenlet” 是一个很小的独立微线程。可以把它想像成一个堆栈帧，栈底是初始调用，而栈顶是当前greenlet的暂停位置。你使用greenlet创建一堆这样的堆栈，然后在他们之间跳转执行。跳转不是绝对的：一个greenlet必须选择跳转到选择好的另一个greenlet，这会让前一个挂起，而后一个恢复。两 个greenlet之间的跳转称为 切换(switch) 。


关于monkey patching 是使其他的python基准库能够使用携程的做法。

主要是用来解决阻塞的。







