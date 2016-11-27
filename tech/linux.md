---
title: "linux"
date: 2015-03-27 16:46
---

[TOC]
# shell && 基本语法

##  基础命令
`if` 语法
    
    for x in $in_list;do
    if [ "$new" == "$x" ]
    then
        echo "same "$x
        continue
    else
        continue
        #sh run.sh $new $x > $root$new"_"$x.log
    fi
    done;
`cp`
    
    默认cp -i 会提示overrite。
    可以先unalias

    不复制指定文件： cp -r `ls| grep -v git`  ~/tmp/text_analysis
    cp -r `ls | grep -v .py*` /home/dongjian/code/text_analysis/classification/short_text/serv/

`grep` [参考链接](https://getpocket.com/a/read/495111387)
    
    在grep 中使用正则的{} 需要转义
    or
        grep -e | egrep 等
    and
        grep -e "a.*b|b*.a"
    not
        grep -v 
`du`
    -B 
`crontab` 
注意的地方： 默认root用户执行。 添加 python path。python 路径。cd 到用户路径操作。

export PYTHONPATH=/home/dongjian/code/
cd /home/dongjian/code/data_serv/user_profile/user_profile
nohup python cal_profile.py  > /home/dongjian/log/cal_profile.log 2>&1 &
nohup python cal_short_interest.py > /home/dongjian/log/cal_short_profile.log 2>&1 &

`vim`

    %s/\\x22/"/g
    %s/\\x5C//g
    g 代表全局。
    s 代表替换

`date`

    date1=$(date --date='1 days ago +%Y%m%d')    #前一天的日期
    date1=$(date --date='2 days ago +%Y%m%d')    #前l两天的日期

    生成日期组
    d="2014-06-29"
    until [[ $d > "2014-07-03" ]]; do // for i in $(req 10) 
        echo "$d"
        d=$(date -I -d "$d + 1 day")
    done

字符串处理
    
    ##*string 删除string 最后一个出现往左的所有字符。

    ${varible##*string} 从左向右截取最后一个string后的字符串
    ${varible#*string}从左向右截取第一个string后的字符串
    ${varible%%string*}从右向左截取最后一个string后的字符串
    ${varible%string*}从右向左截取第一个string后的字符串

链接行 

    使用paste
    paste a b 
## sed

取文章的前n行，后m行。

sed -n 'n,m' a > tmp_dj 


sed -i 's/\\x22/"/g' api.hot.yoka.com.access_20150810.log 


## `AWK` 
    NF 每行的字段数量

随机排列行

    shuf -o 'rs' input


**NF 妙用**

打印倒数第二个字段。

    awk '{print $(NF-1)}'

在awk中大家都知道NF的作用，它是一个awk的内建变量，代表是每行的字段数量。常用的几种方式我给大家慢慢到来。最多的就是在读取每个字段内容 for(i=1;i<=NF;i++) 这个运用非常之多。我们看看高级的几个高级用法：
    $ cat file 
    a b c d
    1 2 3 4
    $ awk -vOFS="|" 'NF+=0' file 
    a|b|c|d
    1|2|3|4
    [解析]
      替换字段分割符，必须要对字段有个action才能使OFS生效，这里我们运用 NF+=0 的方法，即有了操作，而并为改变其原有的值，很巧妙吧。
     
    $ cat file 
    aa
    bb

    cc

    dd
    $ awk NF file 
    aa
    bb
    cc
    dd
    [解析]
      排除空行，因为空行NF=0，0为假不会打印该行。
     
**不打印某一个字段**

    cat file 
    a b c d e f
    1 2 3 4
    awk 'NF-=2' file
    a b c d
    1 2
    awk '{for(i=3;i<NF;i++)printf("%s ",$i);print $NF}' file
    c d e f
    3 4
     
    [解析]
      不输出后面2个字段和前面2个字段。

    不打印某一列
        echo '1 2 3 4 5 6 7' | awk '{$1=$2=$3=""}1' | tr  ' ' '-' 
        ---4-5-6-7
        cat somefile | awk '{$1=$2=""; print $0}'

**截取字符串**
substr(str,start,end)

**分割字符串**

split($0,a,"|")

$0 被分割，
a 后续使用变量。
| 分隔符。


**awk grep**
注意grep的$0 要用“”

    awk '{print $0;a="cat log|grep "$0"|head -n 1";system(a)}'


**引用shell变量**
记得用单引号
## uniq 

**基本用法**

uniq命令

    文件经过处理后在它的输出文件中可能会出现重复的行。例如，使用cat命令将两个文件合并后，再使用sort命令进行排序，就可能出现重复行。这时可以使用uniq命令将这些重复行从输出文件中删除，只留下每条记录的唯一样本。

    语法：

    uniq [选项] 文件

    说明：这个命令读取输入文件，并比较相邻的行。在正常情况下，第二个及以后更多个重复行将被删去，行比较是根据所用字符集的排序序列进行的。该命令加工后的结果写到输出文件中。输入文件和输出文件必须不同。如果输入文件用“- ”表示，则从标准输入读取。

    该命令各选项含义如下：

    - c 显示输出中，在每行行首加上本行在文件中出现的次数。它可取代- u和- d选项。

    - d 只显示重复行。

    - u 只显示文件中不重复的各行。

    - n 前n个字段与每个字段前的空白一起被忽略。一个字段是一个非空格、非制表符的字符串，彼此由制表符和空格隔开（字段从0开始编号）。

    +n 前n个字符被忽略，之前的字符被跳过（字符从0开始编号）。

    - f n 与- n相同，这里n是字段数。

    - s n 与＋n相同，这里n是字符数。

**文件交集、并集**

    1. 取出两个文件的并集(重复的行只保留一份)

    cat file1 file2 | sort | uniq

    2. 取出两个文件的交集(只留下同时存在于两个文件中的文件)

    cat file1 file2 | sort | uniq -d

    3. 删除交集，留下其他的行

    cat file1 file2 | sort | uniq -u

    如果需要计数也有一个很好的参数uniq -c 可以将相同行数的计数放在行首

    sort排序是根据从输入行抽取的一个或多个关键字进行比较来完成的。排序关键字定义了用来排序的最小的字符序列。缺省情况下以整行为关键字按ASCII字符顺序进行排序。

    改变缺省设置的选项主要有：

    - m 若给定文件已排好序，合并文件。

    - c 检查给定文件是否已排好序，如果它们没有都排好序，则打印一个出错信息，并以状态值1退出。

    - u 对排序后认为相同的行只留其中一行。

    - o 输出文件 将排序输出写到输出文件中而不是标准输出，如果输出文件是输入文件之一，sort先将该文件的内容写入一个临时文件，然后再排序和写输出结果。

    改变缺省排序规则的选项主要有：

    - d 按字典顺序排序，比较时仅字母、数字、空格和制表符有意义。

    - f 将小写字母与大写字母同等对待。

    - I 忽略非打印字符。

    - M 作为月份比较：“JAN”<“FEB”

    - r 按逆序输出排序结果。

    -k, -key=POS1[,POS2] posl - pos2 指定一个或几个字段作为排序关键字，字段位置从posl开始，到pos2为止（包括posl，不包括pos2）。如不指定pos2，则关键字为从posl到行尾。字段和字符的位置从0开始。
    参考链接 : http://roclinux.cn/?p=1472

    - b 在每行中寻找排序关键字时忽略前导的空白（空格和制表符）。

    - t separator 指定字符separator作为字段分隔符。

    

sed -s 

**用户权限**
    
    chmod
    chown [-R] 账号名称 文件或目录
    chgrp -R
chown [-R] 账号名称:用户组名称 文件或目录


##  关于前后台的命令 

fg、bg、jobs、&、nohup、ctrl+z、ctrl+c 命令

一、&

    加在一个命令的最后，可以把这个命令放到后台执行，如

    watch  -n 10 sh  test.sh  &  #每10s在后台执行一次test.sh脚本
二、ctrl + z`

    可以将一个正在前台执行的命令放到后台，并且处于暂停状态。

三、jobs

    查看当前有多少在后台运行的命令

    jobs -l选项可显示所有任务的PID，jobs的状态可以是running, stopped, Terminated。但是如果任务被终止了（kill），shell 从当前的shell环境已知的列表中删除任务的进程标识。

四、fg

    将后台中的命令调至前台继续运行。如果后台中有多个命令，可以用fg %jobnumber（是命令编号，不是进程号）将选中的命令调出。



五、bg

    将一个在后台暂停的命令，变成在后台继续执行。如果后台中有多个命令，可以用bg %jobnumber将选中的命令调出。

六、kill

    法子1：通过jobs命令查看job号（假设为num），然后执行kill %num
    法子2：通过ps命令查看job的进程号（PID，假设为pid），然后执行kill pid
    前台进程的终止：Ctrl+c

七、nohup

    如果让程序始终在后台执行，即使关闭当前的终端也执行（之前的&做不到），这时候需要nohup。该命令可以在你退出帐户/关闭终端之后继续运行相应的进程。关闭中断后，在另一个终端jobs已经无法看到后台跑得程序了，此时利用ps（进程查看命令）

    ps -aux | grep "test.sh"  #a:显示所有程序 u:以用户为主的格式来显示 x:显示所有程序，不以终端机来区分

###     Linux运行与控制后台进程的方法：nohup, setsid, &, disown, screen
1.nohup

    顾名思义，nohup的用途就是让提交的命令忽略所有的hangup信号。
    使用方法：nohup COMMAND [ARG]...

2.setsid

    在一个新的会话中运行命令，从而可以避开当前终端发出的HUP信号。
    使用方法：setsid COMMAND [ARG]...

3.&

    可以结合()产生一个新的子shell并在这个子shell中将任务放置到后台运行，从而不受当前shell终端的HUP信号影响。
    使用方法：(COMMAND [ARG]... &)
    
    而我通常的使用方式为：
    nohup ./filename.sh > filename.log 2>&1 &
    三点理由:
    1)nohup保障进程不会被hangup信号异常中断；
    2)将任务放置到后台运行，不占用当前的终端；
    3)将错误输出也打印到log中，默认>只有标准输出，错误输出没有。
    
    
4.控制进程

    通过以下命令，我们可以对放入到后台的命令进行控制
    
    查看当前终端下的后台进程：
    直接执行：jobs
    
    将查看到的某个后台进程放回到前台：
    直接输入：fg {jobid} //这里的{jobid}是通过jobs命令中看到的进程前[]中的数字。
    
    将当前正在前台运行的进程放到后台运行:
    先敲下快捷键：ctrl +z //暂停当前正在运行的进程。
    再执行：bg
    
    终止当前正在前台运行的进程：
    直接敲下快捷键：ctrl +c
    
5.disown

    亡羊补牢，为没有使用nohup与setsid的进程加上忽略HUP信号的功能。
    使用方法：
    将当前正在前台运行的进程放到后台运行（ctrl+z和bg）;
    然后执行disown -h %{jobid} //这里的{jobid}是通过jobs命令中看到的进程前[]中的数字。
    
6.通过screen来实现稳定的后台运行

    screen是建立一个新的全屏虚拟会话终端，这个会话只有在手动输入exit的时候才会退出，在这个会话里执行的命令不用担心HUP信号会对我们的进程    造成影响，因此也不用给每个命令前都加上“nohup”或“setsid”了，非常适合我们有规划的执行大量的后台任务，可以非常方便的让我们对这些后台任   务进行管理。
    
    使用方法：
    screen //立即创建并进入一个会话。
    screen -dmS {name} //建立一个处于断开模式下的会话，并根据我们的需要指定其会话名称。
    screen -list //列出所有会话。
    screen -r {name} //进入指定会话。
    ctrl +ad //输入快捷键ctrl +a和d，可暂时退出当前会话。
    exit //进入指定会话后执行exit即可关闭该会话。
##  问题 ##
linux 乱码问题 查看locale 全部修改为en_US.UTF-8

linux 读取windows 乱码问题 iconv -f gbk -t utf8 README.txt > README.txt.utf8

关于2>&1 和 & 位置的问题 
    &毫无疑问放到最后，否则2>&1 怎么都不起作用。

关于2>&1 和 >  tmp.log 的问题。
    毫无疑问是放到 > tmp.log 之后的。


删除乱码文件。
    
    http://www.longhui.org/archives/445
    

解决less 乱码问题 

    export LESSCHARSET=latin1
##  快捷 ##
2. 给出用户名，用一行shell 命令kill掉所有该用户所有进程。
    ○ 参考答案：
        § 用户名：kobe
        ps -ef | grep kobe | grep -v 'grep\|sshd' | awk '{print $2}' | xargs -i kill {}
    
多个字段匹配

    grep -E "svm|Accuracy"

###     上传公钥 

SSH Keys
SSH key 可以让你在你的电脑和 Git @ OSC 之间建立安全的加密连接。

你可以按如下命令来生成sshkey

ssh-keygen -t rsa -C "xxxxx@xxxxx.com"# Creates a new ssh key using the provided email
     Generating public/private rsa key pair...
查看你的public key，并把他添加到 Git @ OSC http://git.oschina.net/keys

cat ~/.ssh/id_rsa.pub
    ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC6eNtGpNGwstc....
添加后，在终端（Terminal）中输入

ssh -T git@git.oschina.net
若返回

Welcome to Git@OSC, yourname! 
则证明添加成功。
