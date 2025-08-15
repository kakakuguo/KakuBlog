---
title: linux常用指令
description: 本文介绍了在linux中的常用指令
pubDate: 2025 08 07 22:21
categories:
  - Others
tags:
  - linux
  - CentOS
  - Kaku
---

## 基础指令

Linux下的指令可以通过tab键进行自动补全。Ctrl+c可以打断指令执行，如果指令执行的很快并且不需要确认的，一般是打不断的。

> 下面的命令都是在CentOS7.8的环境下测试的,其他Linux版本不一定都能成功运行

### touch(创建文件)

```shell
例子1： touch 1.txt           #创建单个文件
例子2： touch test{1..10}.txt #批量创建文件touch test{a..f}.txt
例子3： touch /root/4.txt     #在指定的/root目录下，创建文件4.txt# 如果touch的文件名称重复了，不会覆盖原文件
```

### ls(查看目录下的文件)

```shell
# ls全称list
例子1：ls test09.txt   #查看test09.txt是否存在，有会显示文件名称，没有会报错
例子2：ls *.txt        #查看以txt结尾的所有文件，类似于windows下的*.后缀名搜索
例子3：ls  -1          #以一行一个文件的方式显示，注意这是-1，是数字1，不是l昂
例子4：ls  -a          #查看所有文件，包括隐藏文件，touch .文件名，.开头的就是隐藏文件
例子5：ls -a -1        #查看所有文件，以一行一个来显示
例子6：ls -l   		#类似于windows的详细列表，这个-l不是数字1
例子7：ls -lh   		#将文件详细显示并文件大小以人类可读的方式显示。超过1024B会显示1k，超过1024K会显示1G
```

### move(移动、也可以进行重命名)

```shell
# mv全称move
例子1：mv 222.txt 123.txt    #将222.txt文件重命名为123.txt
例子2：mv 123.txt /opt       #将当前目录下的123.txt移动到/opt目录下
重命名：mv kaku kaku2 # 将kaku目录改名为kaku2
```

### cp(复制)

```shell
#cp全称copy，windows下复制有个特点，就是如果复制到的文件夹中有同名的文件，会帮我们改名字并加上副本两个字，但linux不会帮我们改名字，我们需要自己指定名字，后缀名尽量不要改。
例子1：cp test01.txt /opt/   #将当前目录下的test01.txt复制到/opt目录下
例子2：cp -a dev04 /opt/     #将目录dev04复制到/opt下，注意，要在dev04的上一级目录来复制它，在它内部是不能复制这个文件夹的，相当于-dpr
例子3：cp -a -v /root /root2  # -v是显示拷贝过程的，-a 保留原文件属性的前提下复制文件
```

### rm(删除)

```shell
#注意Linux和windows不同，没有回收站，删了就是删了
例子1:  rm /opt/123.txt        #将/opt目录下的123.txt文件删除，需要回复y确认删除
例子2： rm -f /opt/test01.txt  #将/opt目录下的test01.txt文件删除，不需要回复，强制删除，很多指令都有自己的参数，而且有好多，-f就是强制的意思。
例子3： rm 文件1 文件2 文件3     #删除多个文件
rm -r dev                     #删除一个目录，linux的参数大部分没有先后顺序#直接删除文件夹，比如 rm dev，这是不行的，会报错，需要带上r参数
[root@localhost ~]# rm -f -r dev02 
[root@localhost ~]# rm -r -f dev03
[root@localhost ~]# rm -fr dev # rm的两个参数可以合并到一起[root@localhost ~]# rm -rf dev01
```

### mkdir(创建文件夹)

```shell
#创建文件夹 创建目录directory，这里说的目录就是文件夹，默认显示是蓝色的字体，文件显示是白色的字
体
# mkdir 全称make directory 
例子1：mkdir dev   #创建一个dev目录
例子2：mkdir dev{01..10}     #批量创建多个目录
例子3：mkdir -p 1/2/3/4/5/6  #一次性创建多级子目录
```

### cd(切换目录)

```shell
cd  #全称change directory
例子1：cd local    #切换到local目录中
例子2：cd /usr/local  #切换到目录/usr/local
例子3：cd ..       #切换到上一级目录
例子4：cd ../..  # 进入上一级的上一级目录 ，还可以继续../
例子5: cd /  # 直接切换到根目录
```

### pwd(显示当前工作目录)

```shell
pwd #打印当前工作目录
```

### history(历史指令查询)

```shell
# 历史指令查询
history
```

### 目录分隔符(/)

```shell
windows：C:\Users\ls198\Desktop # 微软故意用\，其他的unix分支系统都是/来分割
linux：/root/kaku/xx
linux只有一个盘符，不像windows，可以设置c盘、d盘...
/是根目录
/root 根目录下面的root目录
/root/kaku/root/kaku/xx
```

### vi(修改文件内容)

```shell
#vi编辑器，和windows的记事本工具类似
例子1： vi test03.txt   #编辑文件test03.txt,不存在该文件会创建一个空文件
# vi编辑保存文件，需要三种模式切换
常规模式：默认是常规模式，在常规模式中可以使用各种快捷键，帮我们快速编辑文件，比如dd，就是删除当前一行数据
编辑模式：切换英文输入法，然后按ioa三个键中的任意一个键都可以进入编辑模式，这样才能向文件中写内容，写完内容之后，先回到常规模式，在编辑模式中按esc回到常规模式
命令模式：在常规模式时按:(英文的冒号)进入命令模式，命令模式按esc回到常规模式，命令模式下输入q然后回车表示退出文件，wq保存并退出，q!表示强制退出不保存
```

### cat(查看文件内容)

```shell
# vi可以查看文件内容，但是每次都要vi进去，看完再退出来，比较麻烦，如果只是查看文件内容，如下指令即可。
例子1： vi test03.txt   #编辑文件test03.txt
例子2：cat test03.txt  #查看test03.txt的全部内容
例子3：cat -n kaku.txt # 显示内容的同时，显示行号
#从下往上倒着查看文本内容
tac例子1：tac test03.txt  #倒着查看test03.txt的全部内容
```

### head(查看文件头部几行)

```shell
例子1： head test03.txt       #查看文件的前十行，默认
例子2： head  -n 5 test03.txt  #查看文件的前5行
例子3： head  -5 test03.txt   #查看文件的前5行
```

### tail(查看文件后几行)

```shell
#查看文件倒数几行
例子1： tail test03.txt        #查看文件的倒数十行，默认
例子2： tail  -n 5 test03.txt  #查看文件的倒数5行
例子3： tail  -5 test03.txt   #查看文件的倒数5行
```

### 管道符(|)

```shell
# 管道符号： | ，可以将前面指令的执行结果，作为后面指令的操作内容。
# 比如我们通过管道来过滤出ip地址：
[root@localhost ~]# ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group 
default qlen 1000
   link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
   inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
   inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP 
group default qlen 1000
   link/ether 00:0c:29:83:e4:d9 brd ff:ff:ff:ff:ff:ff
   inet 10.0.0.128/24 brd 10.0.0.255 scope global noprefixroute dynamic ens33
       valid_lft 1253sec preferred_lft 1253sec
   inet6 fe80::ffe1:31ed:56dc:d9aa/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
       
[root@localhost ~]# ip addr|tail -4
   inet 10.0.0.128/24 brd 10.0.0.255 scope global noprefixroute dynamic ens33
       valid_lft 1224sec preferred_lft 1224sec
   inet6 fe80::ffe1:31ed:56dc:d9aa/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
       
[root@localhost ~]# ip addr|tail -4|head -1
   inet 10.0.0.128/24 brd 10.0.0.255 scope global noprefixroute dynamic ens33
    
[root@localhost ~]# ip addr|tail -4|head -1|cut -c 10-19 # cut -c 10-19表示从第10
10.0.0.128
个字符显示到第19个字符，这个指令可以忽略，大致了解一下即可，因为字符长度不固定，切的时候有可能切
不准确
```

### wc(统计文件信息)

```shell
#统计，比如统计文件有多少个字节、多少行等等
wc  #全称Word Count，计数
wc -l # 按行统计
wc -c # 按字符统计
[root@localhost ~]# cat kaku.txt |wc -l  # 共18行
18
```

### seq(生成数字序列)

```shell
seq # 全称：sequence，序列的意思
例子1：产生一个5到12的序列
[root@localhost ~]# seq 5 12
5
6
7
8
9
10
11
12
例子2：产生一个5到12等宽的序列
[root@localhost ~]# seq -w 5 12
05
06
07
08
09
10
11
12
```

### grep(按行过滤字符串)

```shell
# 默认是模糊匹配，按行过滤字符串，只要单词中含有某些内容就过滤出单词所在的每行数据
例子1： #普通过滤，将含有3这个字符的行过滤出来
[root@localhost ~]# grep '333' kaku.txt 
33333
33334
33333
53333
例子2： #显示行号
[root@localhost ~]# grep -n '333' kaku.txt 
8:33333
10:33333
12:3333314:33333

# 可以借助正则表达式来进行过滤，可以将内容过滤的很精确，有些在线的网站也可以帮我们生成一些常用的
正则表达式，比如https://www.hake.cc/tools/regexcode/
[root@localhost ~]# grep 'Failed password' /var/log/secure|grep --color -P "
(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)\.(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)\.
(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)\.(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)"
Mar 25 18:20:48 localhost sshd[16905]: Failed password for root from
192.168.61.1 port 55577 ssh2
# ip地址都标红色了，表示匹配出来了。
# 如果只要ip地址-Po
[root@localhost ~]# grep 'Failed password' /var/log/secure|grep --color -Po "
(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)\.(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)\.
(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)\.(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)"
192.168.61.1
# 有些ip地址是重复的，因为尝试登录了很多次，那么可以先排序，再去重，来查看ip地址
[root@localhost ~]# grep 'Failed password' /var/log/secure|grep --color -Po "
(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)\.(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)\.
(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)\.(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?
\d)"|sort -n |uniq -c
2 192.168.2.113
3 192.168.2.116
1 192.168.61.1

#grep参数
-n 显示行号
[root@localhost ~]# grep -n 'tcp' test.txt
# vi test.txt +48，表示进入vi的时候，光标直接定位的48行起始位置。
-c 对结果行计数
[root@localhost ~]# grep -c 'tcp' test.txt
14
-i 不区分大小写
[root@localhost ~]# grep -n 'tcp' test.txt -i
-v 反向搜索，取反
[root@localhost ~]# grep -n 'udp' test.txt -v # 将不含有udp的行全部过滤出来
-w 精准匹配
[root@localhost ~]# grep -w 'tcp' test.txt
-o 只显示匹配的结果，前面的第一个示例中我们用过-o参数
[root@localhost ~]# grep -o -n 'tcp' test.txt
-A1 同时打印搜索结果行的后一行 ，A是after的简写
[root@localhost ~]# grep -A2 'ftp' test.txt
[root@localhost ~]# grep -A 2 'ftp' test.txt
-B3 同时打印搜索结果行的前三行，B是before的简写
[root@localhost ~]# grep -B2 'ftp' test.txt
-C2 同时打印搜索结果行的上下各两行
[root@localhost ~]# grep -C2 'ftp' test.txt
-E 扩展正则表达式
# 正则我们下面会细讲，先简单了解一下。
[root@localhost ~]# grep -E '.tp' test.txt # .就是正则表达式，表示任意的一个字符
[root@localhost ~]# grep -E 'ftp|ssh' test.txt # 查找ftp或者ssh，|是或者的意思，
可以用多个ftp|ssh|telnet...
-P 使用perl正则
# perl语言中设计的正则表达式写法规则，很强大，很多领域都支持perl正则的语法结构。
[root@localhost ~]# grep -P "\d+" test.txt # 匹配所有的数字
[root@localhost ~]# grep -P "\d{4,}" test.txt #匹配4位的数字
```

### sed(取行和修改替换)

```shell
#擅长取行和修改替换
用法：sed [-nri] [动作] 目标文件文件
选项与参数：
-n ：使用安静(silent)模式。在一般 sed 的用法中，所有来自 STDIN 的数据一般都会被列出到终端
上。但如果加上 -n 参数后，则只有经过sed 特殊处理的那一行(或者动作)才会被列出来。
-r ：sed 的动作支持的是延伸型正则表示法的语法。(默认是基础正则表示法语法)
-i ：直接修改读取的文件内容，而不是输出到终端。
动作说明： [n1[,n2]]function
n1, n2一般表示为行号，[,n2]表示这个参数可选，可有可无。
function：
a ：指定行后面插入一行
d ：删除
i ：指定行前面插入一行
p ：打印，#一般和前面的-n参数一起用
s ：替换 需要I忽略大小写，全局替换需要g
sed过滤
# sed也可以进行过滤，如下简单示例
[root@localhost ~]# seq 5 > 1.txt
[root@localhost ~]# vi 1.txt # 修改为如下内容
[root@localhost ~]# cat 1.txt
1
2c
3a
4b
5a
[root@localhost ~]# sed '/a/p' 1.txt #默认会将所有行都打印出来，并且匹配到的a所在的
行重新打印一遍
1
2c
3a
3a
4b
5a
5a
[root@localhost ~]# sed -n '/a/p' 1.txt # 加上-n，进入安静(silent)模式，就不会
将所有内容打印出来了。
3a
5a
# sed过滤相比grep来说，就比较麻烦。所以，过滤我们一般用grep。
[root@localhost ~]# sed -n '/tcp/p' test.txt # 也能过滤出tcp所在的行
# sed删除匹配的行数据
[root@localhost ~]# sed '/tcp/d' test.txt # 删除所有带tcp的行，并不是删除原文件
中的数据，而是将删除之后的结果打印出来了。
# 所以只需要一个重定向，就拿到删除之后的结果了
[root@localhost ~]# sed '/tcp/d' test.txt > 2.txt
[root@localhost ~]# cat -n 2.txt
# -i就可以直接删除原文件的数据
[root@localhost ~]# sed -i '/tcp/d' test.txt
[root@localhost ~]# cat -n test.txt
[root@localhost ~]# sed -i '/udp/d' test.txt
[root@localhost ~]# cat -n test.txt
[root@localhost ~]# sed '/^#/d' test.txt # 删除以#开头的行，^表示以什么开头的正则表达式，我没有加-i昂
# 指定行号来删除
[root@localhost ~]# sed '1,10d' test.txt # 删除1-10行的数据
[root@localhost ~]# sed -i '1,10d' test.txt
# 只要1-5行的数据
[root@localhost ~]# sed -n '1,5p' test.txt
# 只要第5行的数据
[root@localhost ~]# sed -n '5p' test.txt
# 插入数据
# 在第三行后面插入一行数据
[root@localhost ~]# sed '3a hello kaku' 1.txt
1
2c
3a
hello kaku
4b
5a
# 在第2行前面插入一行数据
[root@localhost ~]# sed '2i hello kaku' 1.txt
1
hello kaku
2c
3a
4b
5a
# 加上-i参数就能直接修改原文件
[root@localhost ~]# sed -i '2i hello kaku' 1.txt
[root@localhost ~]# cat 1.txt
1
hello kaku
2c
3a
4b
5a
# 替换数据
# 把3a替换成wuLAOBAN
[root@localhost ~]# sed 's#3a#wuLAOBAN#' 1.txt
1
hello kaku
2c
wuLAOBAN
4b
5a
[root@localhost ~]# sed -i 's#3a#wuLAOBAN#' 1.txt
[root@localhost ~]# cat 1.txt
1
hello kaku
2c
wuLAOBAN
4b
5a
# 把A替换成xxx，每行只替换一次，同一行的第二个及之后的A都不进行替换
[root@localhost ~]# sed 's#A#xxx#' 1.txt
1
hello kaku
2c
wuLxxxOBAN
4b
5a
# 把所有的A都替换成xxx
[root@localhost ~]# sed 's#A#xxx#g' 1.txt
1
hello kaku
2c
wuLxxxOBxxxN
4b
5a
# 把所有的A和a都替换成xxx，忽略大小写，参数I
awk
[root@localhost ~]# sed 's#A#xxx#gI' 1.txt
1
hello jxxxden
2c
wuLxxxOBxxxN
4b
5xxx
# -r参数也是和正则搭配来用的，grep是-E和-P参数
```



### awk(按列过滤字符串)

```shell
awk #awk其名称得自于它的创始人 Alfred Aho 、Peter Weinberger 和 Brian Kernighan 姓氏的首个字母。
# 取列,$1代表第一列，$2代表第二列，$NF代表最后一列，列是由空格分开的
例子1： 
[root@localhost ~]# cat kaku.txt 
row 1, cell 1 row 1, cell 2
row 2, cell 1 row 2, cell 2
[root@localhost ~]# awk '{print $1}' kaku.txt # 注意，必须是单引号
row
row
[root@localhost ~]# awk '{print $2}' kaku.txt 
1,
2,
例子2：以逗号,做分隔符
[root@localhost ~]# cat kaku.txt 
row 1, cell 1 row 1, cell 2
row 2, cell 1 row 2, cell 2
[root@localhost ~]# awk -F ','   '{print $1}' kaku.txt 
row 1
row 2
[root@localhost ~]# awk -F ','   '{print $NF}' kaku.txt 
 cell 2
 cell 2
 
 # 擅长取列
用法，取列
例子1： 取列
[root@localhost ~]# vi 3.txt
[root@localhost ~]# cat 3.txt
2 this is a test
3 Do you like awk
This's a test
10 There are orange,apple,mongo
[root@localhost ~]# awk '{print $1}' 3.txt
2
3
This's
10
[root@localhost ~]# awk '{print $3}' 3.txt # 取第三列
[root@localhost ~]# awk '{print $NF}' 3.txt # 取每一行的最后一列，NF是固定写法
test
awk
test
orange,apple,mongo
[root@localhost ~]# awk '{print $1,$NF}' 3.txt # 取第一列和最后一列
2 test
3 awk
This's test
10 orange,apple,mongo
[root@localhost ~]# awk '{print $NF,$1}' 3.txt # 还可以反着写，所以通过awk，可以
将列顺序重新排版
[root@localhost ~]# awk '{print $1,$4}' kaku.txt # 取出第一列和第四列
例子2：计算
vi 4.txt，写上如下内容
# 水果，每斤多少钱，总共多少斤
orange 10 20
apple 20 30
mongo 50 10
banana 5 200
# 开始计算
[root@localhost ~]# awk '{print $1,$2*$3}' 4.txt
orange 200
apple 600
mongo 500
banana 1000
# 还可以加备注信息：
[root@localhost ~]# awk '{print $1"总价为：",$2*$3"元"}' 4.txt
orange总价为： 200元
apple总价为： 600元
mongo总价为： 500元
banana总价为： 1000元
# 例子3：根据行号来筛选内容
# a = 1表示变量赋值，让a=1
# a == 1，表示判断一下a的值是不是等于1，等于1那么条件判断结果为真，不等1那么条件判断结果为假
# 支持符号： > < == >= <=
[root@localhost ~]# awk 'NR==1' 4.txt # 取出第一行数据，grep不会取出特定的行，只能筛选
某些行
orange 10 20
[root@localhost ~]# awk 'NR>2' 4.txt # 取出行号大于2的行数据
mongo 50 10
banana 5 200
[root@localhost ~]# awk 'NR<=3' 4.txt # 取出行号小于等于3的行数据
orange 10 20
apple 20 30
mongo 50 10
[root@localhost ~]# awk 'NR<=3 && NR>1' 4.txt # 取出行号大于1并且小于等于3的行
apple 20 30
mongo 50 10
# 还可以取行的同时来取列
[root@localhost ~]# awk 'NR<=3{print $1}' 4.txt
orange
apple
mongo
# 例子4：
# 还可以过滤出指定的行，awk也能做过滤，但是
[root@localhost ~]# awk '/apple/' 4.txt # 取出含有apple数据的行数据
apple 20 30
# grep、sed、awk过滤对比
grep 'apple' 4.txt
sed -n '1,2p' 4.txt
awk 'NR>1 && NR<=3' 4.txt
# 例子5：
# 再比如我们刚才取ip地址：比直接写正则要方便很多
[root@localhost log]# grep 'Failed password' secure
Mar 25 18:20:48 localhost sshd[16905]: Failed password for root from
192.168.61.1 port 55577 ssh2
Mar 25 18:49:26 localhost sshd[1498]: Failed password for root from
192.168.2.113 port 49991 ssh2
...
[root@localhost log]# grep 'Failed password' secure|awk '{print $11}'
192.168.61.1
192.168.2.113
192.168.2.116
...
# 例子6： 指定分隔符，默认是按照空格作为分隔符的
awk -F ":" '{print $7,$1}' /etc/passwd # 这个文件都是用:做的分隔符
[root@localhost ~]# awk -F ':' 'NR==3 || NR==5 {print $1}' /etc/passwd # 取出第三
行和第五行的第一列数据，分隔符为:
daemon
lp
# &&表示and，两个条件同时成立
# ||表示or，满足一个条件即可
# 例子7： 拼凑指定文本,双引号之间原样输出
# awk -F ":" '{print $1":123:"$7}' /etc/passwd
[root@localhost ~]# awk -F ":" '{print $1":123:"$7}' /etc/passwd
root:123:/bin/bash
bin:123:/sbin/nologin
...
# 例子8: 过滤文本
# awk -F "[ /]+" '$2~/^47/' 1.txt
# 找出第一列数据中带h的，并取出第一列和第七列的数据
[root@localhost ~]# awk -F ':' '$1~/h/{print $1,$7}' /etc/passwd
shutdown /sbin/shutdown
halt /sbin/halt
sshd /sbin/nologin
chrony /sbin/nologin
apache /sbin/nologin
```

### vi/vim编辑器

vi和vim的快捷键是通用的。系统默认是安装了vi的，而vim需要我们自己去装(yum install vim -y)，加强版的vi，功能更强。

#### 移动光标

```shell
[root@localhost ~]# vi services 
set number # 显示出行号
左，下，上，右，如果键盘上没有上下左右键，可以h,j,k,l 
进入编辑模式有三个按钮：i、a、o， i在光标位置编辑、a是在光标后一位编辑、o是换行编辑，新起一行
ctrl+f 下翻一页
ctrl+b 上翻一页
ctrl+u 上翻半页
ctrl+d 下翻半页
0 跳至行首，不管有无缩进，就是跳到第0个字符
^ 跳至行首的第一个字符
$ 跳至行尾(shift+4)
gg 跳至文首
G 跳至文尾(shift+g)
5gg/5G 调至第5行，或者命令行模式:5回车，也是跳到第5行，所以其实操作命令都不是唯一的
```

#### 删除复制

```shell
x删除单个字符
10x删除10个字符
dd 删除光标所在行(其实dd是剪切的操作),  #使用u撤销之前的操作，使用ctrl+r恢复
6dd 从光标开始往下删除6行
dw 删除一个单词(word)
小p 粘贴粘贴板的内容到当前行的下面，比如将dd剪切的行黏贴到下面
大P 粘贴粘贴板的内容到当前行的上面
yy 复制行
5yy复制5行，复制的内容可以通过p\P来黏贴
```

#### 搜索和替换

```shell
搜索：
   /pattern 向后搜索字符串pattern  #辅助小n向下和大N向上，一般都是用/来搜索
   ?pattern 向前搜索字符串pattern  #辅助小n向上和大N向下，?搜索用的少
替换：
 :1369s/shell/jaden/g  # 将第1369行的shell替换为jaden，/还可以用#或者@符号来代
替：:1369s#shell#jaden#g
 :1369,1379s/shell/jaden/g  # 将1369至1379这10行中的shell替换为jaden
 :1369,$s/shell/jaden/g  # 将1369至文末中的shell替换为jaden
   :%s/old/new/g  #搜索整个文件，将所有的old替换为new
   :%s/old/new/gc #搜索整个文件，将所有的old替换为new，每次都要你确认是否替换(y/n/a/..)，
y表示确认替换一个、n表示不替换、a表示全部替换
```

#### 退出编辑器

```shell
:w 将缓冲区写入文件，即保存修改到硬盘上，但是不退出vi，如果我们改到一半的时候可以提前保存一下，
以防断电，因为新编辑的数据是在内存中的，而且vi不会自动保存。
:wq 保存修改并退出
:x 保存修改并退出，和wq一样的效果。
:q 退出，如果对缓冲区进行过修改，则会提示
:q! 强制退出，放弃修改
:wq! 强制保存修改并退出
```

> 当我们用vi/vim编辑文件aaa.txt时,会自动生成一个.aaa.txt.swp隐藏文件,我们修改后的内容会自动保存到这个文件中,当我们退出时该文件会自动删除。但当非正常退出文件时,这个文件不会自动删除,当再次用vi/vim编辑时会提示该临时文件已存在,这时可以用`vi -r aaa.txt`打开自己之前修改后的内容,再保存即可。

### 正则表达式

```shell
# 准备示例：[root@localhost ~]# head -100 /etc/services > test.txt
1) ^ 表示搜索以什么开头
[root@localhost ~]# grep '^#' test.txt # 找出开头为#号的的行数据
[root@localhost ~]# grep -v '^#' test.txt # 找出开头不是#号的行数据
2) $ 表示搜索以什么结尾。
[root@localhost ~]# grep 'ol$' test.txt # 找出结尾为ol字母的行数据
3) ^$ 表示空行，不是空格。
[root@localhost ~]# grep '^$' test.txt # 找出所有的空白行。
[root@localhost ~]# grep -v '^$' test.txt # 找出所有的非空白行数据，如果保存一下，
那么相当于快速删除所有空行。
# sed删除空行，更容易，因为它更擅长修改文件内容
[root@localhost ~]# sed '/^$/d' test.txt # 加上-i就改了原文件
4) . 代表且只能代表任意一个字符。跟癞子斗地主中的癞子一样。
[root@localhost ~]# grep '.dp' test.txt # 找出xdp，x可以是任意一个字符，注意，是一
个！
5) \ 转义字符，让有着特殊身份意义的字符，脱掉马甲，还原原型。
例如：\.只表示小数点，还原原始小数点的意义。
[root@localhost ~]# grep '\.ia' test.txt # 这就表示，找到含有.dp的行数据
6) * 重复0个或多个前面的一个字符。不代表所有了。
# 准备一个测试数据：
[root@localhost ~]# vi num.txt
[root@localhost ~]# cat num.txt
a 12222
b 12222222
c 1
b 3
d 122222222222222
e 12
a 4
# 看下面几个的效果就知道*的意思了。
[root@localhost ~]# grep '2' num.txt
[root@localhost ~]# grep '22' num.txt
[root@localhost ~]# grep -o '22' num.txt # -o就能看出来，它是两个字符两个字符的匹
配
[root@localhost ~]# grep '12' num.txt
[root@localhost ~]# grep '12*' num.txt
[root@localhost ~]# grep '.*' num.txt # 匹配所有字符
[root@localhost ~]# grep '12.*' num.txt
7) .* 匹配所有的字符。^.* 任意多个字符开头。
[root@localhost ~]# grep '12.*' num.txt
# 小任务：
# 1.复制一份/etc/services的前100行数据到serv文件中，然后将去掉serv文件中所有含有#的行和空行
[root@localhost ~]# head -100 /etc/services > serv
# 用sed来玩：
[root@localhost ~]# sed '/#/d' serv # 去掉含有#号的行
[root@localhost ~]# sed '/^$/d' serv # 去掉所有空行
# 用grep来玩：
[root@localhost ~]# grep -Ev '^$|#' serv > ss.txt
[root@localhost ~]# cat ss.txt
# 2. 去掉aaa.txt文件中所有的空行和注释(注意：一行中可能只有部分是注释)
[root@localhost ~]# cat aaa.txt
hello -a #a表示友好
hello -b #b表示不友好
hello -c #c表示骂人
# 哈哈,这是个啥
# what?
hello -d #d表示非常爱你
[root@localhost ~]# grep '#.*' aaa.txt # 这么写，可以将所有#号注释的内容全部匹配到，所
以这个正则表达式可以用
[root@localhost ~]# sed -i 's/#.*//g' aaa.txt # 将#.*匹配到的内容全部替换为空。
[root@localhost ~]# sed -i '/^$/d' aaa.txt # 再去除空行
[root@localhost ~]# cat aaa.txt # 结果就ok了。
hello -a
hello -b
hello -c
hello -d
8) [abc] 匹配字符集合内任意一个字符[a-z]、[0-9]、[A-Z]，多选一，[0,9]这个是2选1.
[root@localhost ~]# grep -E '[0-9]' serv
[root@localhost ~]# grep -E '[0,9]' serv
9) [^abc] ^在中括号里面表示非，不包含a或b或c。
[root@localhost ~]# grep -E '[^0-9]*' serv # 不要数字
[root@localhost ~]# grep -E '[^a-z]' serv # 不要小写字母
[root@localhost ~]# grep -E '[^a-z0-9A-Z]' serv # 不要字母和数字
10) {n,m} 重复n到m次，前一个字符。
#匹配一下ip地址：0.0.0.0 -- 255.255.255.255，这是ip地址的范围，个数上就是7-15个
[root@localhost ~]# grep -Eo '[0-9.]{7,15}' /var/log/secure # 但是如果有个大于7
位的数字，也会被匹配上8888888
[root@localhost ~]# grep -Eo '[0-9.]{7,15}' /var/log/secure|grep '\.'
11） + 重复1次到多次，和*不同
[root@localhost ~]# grep -E '19*' serv
[root@localhost ~]# grep -E '19+' serv
12） ? 重复0次到多次，和*号很像。
[root@localhost ~]# grep -Eo '[0-9]?' serv
13）\d 和[0-9]是一样的，但是它属于perl正则，grep使用perl正则的时候需要用-P参数来指定
[root@localhost ~]# grep -E '\d' 22.txt
[root@localhost ~]# grep -P '\d' 22.txt

```



### sort(排序)

```shell
sort # 默认排序，先数字后字母
# sort -n # 先字母(先小写字母后大写字母)后数字的排序方式，sort -n -r 反向排序
例子1：
[root@localhost ~]# cat test02.txt
3
2
6
4
8
7
5
3
2
1
2
3
4
5
6
9
1
5
7
[root@localhost ~]# cat test02.txt|sort -n
1
1
2
2
2
3
3
3
4
4
5
5
5
6
6
7
7
8
9
```

### uniq(去重)

```shell
uniq  #全称：unique，唯一、去重的意思，但是它是将连续的去重，不会间隔去重，所以最好先排序再去重
例子1：
[root@localhost ~]# cat test02.txt|sort -n|uniq 
[root@localhost ~]# cat test02.txt|sort -n|uniq -c # -c显示重复次数
      2 1
      3 2
      3 3
      2 4
      3 5
      2 6
      2 7
      1 8      
      1 9
```

### logout(退出该账号)

### hostname(临时修改主机名)

```shell
例子1：
[root@localhost ~]# hostname test
#需要重新登录生效
```

### hostnamectl(查看主机的信息)

```shell
[root@localhost ~]# hostnamectl 
   Static hostname: localhost.localdomain
         Icon name: computer-vm
           Chassis: vm
       Machine ID: f8a89169114741a8ac6de82954c5fbcb
           Boot ID: dcf65386ccda42e29699d56101af8cf1
   Virtualization: vmware
 Operating System: CentOS Linux 7 (Core)
       CPE OS Name: cpe:/o:centos:centos:7
           Kernel: Linux 3.10.0-1127.el7.x86_64
     Architecture: x86-64
#永久修改主机名
[root@localhost ~]# hostnamectl set-hostname test
#需要重新登录生效
```

### reboot(重启主机)

### shutdown(关闭计算机)

```shell
例子1：
#立即关机
[root@localhost ~]# shutdown -h now
例子2：
#5分钟之后关机，可以使用shutdown -c取消
[root@localhost ~]# shutdown -h 5
例子3：
#5分钟之后重启系统，可以使用shutdown -c取消
[root@localhost ~]# shutdown -r 5
```

### history历史命令

```shell
例子1:
[root@test 14:32:10 ~]#history
    1  exit
    2  ls
    3 head -1 test03.txt 
    4 head -1 test03.txt|cat
    5 head -1 test03.txt|tac
    6 head -2 test03.txt|tac
    7 head -2 test03.txt|cat
    8 ip addr
    9 ip addr|tail -4
   10 ip addr|tail -4|head -1
   ......
例子2：
#使用!调用历史命令
[root@test 14:32:10 ~]#history|head -5
    1  exit
    2  ls
    3 head -1 test03.txt 
    4 head -1 test03.txt|cat
    5 head -1 test03.txt|tac
[root@test 14:32:26 ~]# !3
 head -1 test03.txt 
#使用!调用mv开头的命令
[root@test 14:42:17 ~]#history 
    1  ls -a -l .bash_history 
    2 history 
    3  ls
    4 history 
    5  mv aaaaa.txt /tmp/
    6 history 
[root@test 14:42:19 ~]#!mv # 按回车，会自动找最近一次执行的mv开头的指令
mv aaaaa.txt /tmp/
mv: 无法获取"aaaaa.txt" 的文件状态(stat): 没有那个文件或目录
例子4：
#清除历史记录
history -c # 这是清除内存中的历史指令
删除主文件夹下面.bash_history  # 这是清除硬盘中的历史指令，内存中的指令会自动备份
到.bash_history中，但是有个延迟，退出登录之后，才会将历史指令同步到硬盘文件中
每个用户家目录下都有一个.bash_history，记录的是自己用户的历史指令。
.bash_history默认记录最近的1000条指令，通过echo $HISTSIZE可以查看，可以配置的更大或者更小一
些，vi /etc/profile
```

### curl和wget(网站下载文件)

```shell
#下载文件
curl
例子1：
#下载文件
curl -o 本地存放路径 文件网址
例如：# 有些网站在后台可能禁了curl下载，导致下载不下来
 curl -o 123.zip https://github.com/nmap/nmap/archive/refs/heads/master.zip
```

```shell
wget 文件网址
# 需要自行安装一下才有这个功能，curl是系统自带的
# yum install -y wget
[root@localhost ~]# wget 
https://github.com/nmap/nmap/archive/refs/heads/master.zip
# wget比curl方便，最起码不需要指定文件名，curl如果不指定文件名路径的话会将文件内容打印在屏幕上
#使用curl和wget的前提是要有网
#检查网络畅通
ping
例子1：ping www.baidu.com
#如果网不通，重启网络服务
systemctl restart network
#查看文件类型
file
例子1：
file 123.zip
```

### scp传输

```shell
#我们准备两台linux虚拟机,主要用于linux和linux服务器之间传输文件，scp要求接受数据的一方要开启了ssh服务端才行，如果你电脑是苹果电脑mac系统，也可以使用scp来传输，mac默认ssh服务端是没有开启的，可以自行开启，客户端是可以直接使用的。windows往linux上面发送文件也可以用scp，但是只能单向的，因为windows上没有ssh服务端。
#把本地文件推送到远程服务端
# 格式： scp 本地文件路径 远程主机用户@远程主机ip地址:远程主机某个目录
scp typora-setup-x64.exe root@10.0.0.128:/tmp
#把远端服务文件拉取到本地
# 格式：scp 远程主机用户@远程主机ip地址:远程主机某个文件路径 本地路径
scp root@10.0.0.128:/tmp/typora-setup-x64.exe .
#win10及以上版本是有scp指令的，win和win之间是不能使用scp互相传文件的，因为windows上默认是没有ssh的服务端的，只有客户端。
# windows使用scp给linux上传文件的时候，文件路径和文件名中不允许出现中文和空格。mac系统也是直接可以使用scp来给linux上传文件的。
```

### rz和sz(上传和下载)

```shell
#上传和下载
rz  #上传
sz  #下载
#需要先安装lrzsz软件包，这个用的比较多
yum install lrzsz  -y
#上传的例子
如果使用xshell，那么直接鼠标拖拽即可，或者执行rz -E选择要上传的文件
#下载的例子
sz /root/test3.tar.gz  # windows上自行选择存储目录
```

### tree(用树的方式查看当前目录结构)

```shell
tree #查看当前目录结构
.
├── dict.rar
├── dict.txt
├── ks-script-VMKXbJ
├── Linux\347\211\271\346\256\212\347\254\246\345\217\267.pdf
├── vmware-root_618-2697467179
├── vmware-root_620-2697598252
├── vmware-root_621-4013788914
├── vmware-root_624-2688750775
├── vmware-root_626-2697073973
├── vmware-root_630-2688619696
├── vmware-root_634-2730496827
├── vmware-root_635-3979839717
├── vmware-root_637-3979708642
├── vmware-root_649-4021719023
└── yum.log
tree 目录#查看该目录路径

```

### ps(查看进程)

```shell
参数1：ps -ef
# pid：全称process id，是进程编号，每次启动某个程序，它的编号可能都不一样，这个是程序启动之后系统随机分配的。
# uid：全称user id，是进程所属用户，也就是哪个用户启动的，我们可以切换个用户执行一下sleep 60，就可以看到效果
# CMD中看到[]括起来的，表示这些都是系统级别的进程，比如一些硬件驱动程序之类的，这些都不要动。不带[]的都是用户级别的。
# ppid：全称parent process id，父进程，记录的是某个进程是由哪个进程创建出来的。可以通过pstree工具来查看从属关系。
# STIME：全称start time，进程的启动时间。
# TTY： 用来显示哪些是本地启动的，哪些是远程终端连接上来启动的。通过w指令可以看到哪些终端登录着主机。只要登录成功一个终端，那就多一个终端。tty1,tty2表示本地登录的用户，pts/0,pts/1表示远程登录的用户
# TIME：这个没啥用
# CMD：这个进程执行了什么指令
```



### pstree(以树的方式查看所有进程和子进程)

```shell
pstree -p # 查看所有进程信息, -p显示进程ID
systemd─┬─NetworkManager─┬─dhclient
        │                └─2*[{NetworkManager}]
        ├─VGAuthService
        ├─abrt-watch-log
        ├─abrtd
        ├─auditd───{auditd}
        ├─crond
        ├─dbus-daemon
        ├─firewalld───{firewalld}
        ├─irqbalance
        ├─login───bash
        ├─polkitd───6*[{polkitd}]
        ├─rsyslogd───2*[{rsyslogd}]
        ├─sshd─┬─sshd───bash───pstree
        │      └─sshd───sshd───bash
        ├─systemd-journal
        ├─systemd-logind
        ├─systemd-udevd
        ├─tuned───4*[{tuned}]
        └─vmtoolsd───{vmtoolsd}
```

### kill和pkill(关闭进程)

```shell
kill pid号
例子1： kill  7851  #使用进程id号，来终止进程
       kill -9 pid号  #强行结束进程,慎用！！！
#批量关闭进程，pkill全称program kill
pkill CMD命令名称
例子1： pkill sleep  #使用进程的命令名称，来终止进程，会中止所有CMD执行着sleep的进程的。
       pkill -9 sleep
       
# kill -9，这个强大和危险的命令迫使进程在运行时突然终止，进程在结束后不能自我清理。危害是导致系统资源无法正常释放，一般不推荐使用，除非其他办法都无效。
```



### find(文件查找)

```shell
#文件查找
例子1：普通查询
find   /etc   -maxdepth 1  -type f  -name "pa*"
命令   目录...   查找深度     类型   文件名称包含  
# -type文件类型：f表示文件，不指定类型的话，文件和目录都会查找
# -maxdepth查找深度：目录层级的意思，不指定的话，就按照最大深度来查找
# "pa*"： *表示匹配任意pa开头的内容，*号还可以写在开头

例子2：按照文件大小查找(单位kMG,k要小写，MG要大写，不带单位就按照B单位来查找)
1.查找大于100M的文件
find / -type f -size +100M 
   [root@localhost tmp]# find / -type f -size +100M 
   /proc/kcore
    find: ‘/proc/1945/task/1945/fdinfo/6’: 没有那个文件或目录  # proc是进程目录，有些进程运行起来之后能看到文件信息，程序运行结束之后，进程文件也消失了，所以看到proc的报错很正常，并且proc的权限很高，不是一般人可以访问的，所以也经常会报权限不够等错误信息，所以以后看到proc的报错直接忽略即可。
    find: ‘/proc/1945/fdinfo/5’: 没有那个文件或目录
   /sys/devices/pci0000:00/0000:00:0f.0/resource1_wc
   /sys/devices/pci0000:00/0000:00:0f.0/resource1
   /var/cache/yum/x86_64/7/updates/gen/primary_db.sqlite
   /usr/lib/locale/locale-archive
   [root@localhost tmp]# ll -h /usr/lib/locale/locale-archive   #大小确实超过了
100M
    -rw-r--r--. 1 root root 102M 3月  15 20:10 /usr/lib/locale/locale-archive
2.查找小于2k的文件  
find /root/nginx-1.20.2 -type f -size -2k
3.查找大于50M同时小于100M的文件
find /  -type f   -size +50M  -and -size -100M
例子3：
忽略大小写查询
find /etc -maxdepth 1  -iname "pa*"  # i是ignore的简写，忽略的意思

例子4：
根据修改时间查找文件  
   [root@localhost ~]# stat 1.txt
     文件："1.txt"
     大小：0         块：0         IO 块：4096   普通空文件
   设备：801h/2049d Inode：67108933   硬链接：1
   权限：(0644/-rw-r--r--) Uid：(    0/   root)   Gid：(    0/   root)
   环境：unconfined_u:object_r:admin_home_t:s0
   最近访问：2023-03-23 09:04:35.339235371 +0800 #Access time
   最近更改：2023-03-23 09:04:35.339235371 +0800 #Modify time
   最近改动：2023-03-23 09:04:35.339235371 +0800 #Change time
   创建时间：-
    
时间参数：atime mtime ctime amin mmin cmin  #(time是按照天来查找，min是按分钟查找)
# 时间单位为天
find /opt -type f -mtime -1   #-1代表一天以内，+1一天以前
# 时间单位为分钟
[root@localhost ~]# find /root -type f -mmin -20
/root/.bash_history
/root/ReadMe.txt
/root/.lesshst
# 查找1天之前，10天之内，修改过的文件
[root@localhost ~]# find /etc/ -type f -mtime +1 -and -mtime -10

例子5： 取反: !
例子：
   [root@localhost ~]# find /root -type f -name "*.txt" # 找名称以.txt结尾的文件
   /root/1.txt
   /root/学习前准备.txt
   [root@localhost ~]# find /root -type f ! -name "*.txt" # 找名称中不是.txt结尾的
文件
   /root/.bash_logout
   /root/.bash_profile
   ...
    
   [root@localhost ~]# mkdir kaku
   [root@localhost ~]# mkdir wulaoban
   [root@localhost ~]# find /root -type f # 找文件
   /root/.bash_logout
   /root/.bash_profile
 ...
 [root@localhost ~]# find /root ! -type f # 找文件夹
   /root/kaku
   /root/wulaoban
   ...
   
例子6：
根据用户来查找文件
   [root@localhost ~]# useradd kaku
   [root@localhost ~]# find / -user kaku # 查找属于kaku用户的所有目录和文件
   ...
   /var/spool/mail/kaku
   /home/kaku
   /home/kaku/.bash_logout
   /home/kaku/.bash_profile
   /home/kaku/.bashrc
根据用户组来查
   [root@localhost ~]# find / -group kaku
   ...
   
例子7：
对找出的文件进行处理
# 格式：正常的find语句+操作exec
# 比如我们查找到了一些病毒文件，想直接删除  
# find /tmp -type f -size +10K -exec rm rf {} \; # {}表示我们找到的那些文件，\;是这样
的：正常exec语句最后要分号结尾，但是分号在linux中有特殊的意义，比如一次性执行两个指令可以 ls -
lh;id，这样执行，所以要对;进行转义，意思是不要将;作为shell指令的分隔符，\就是转义符号。
例子：
   [root@localhost tmp]# find /tmp -name "vm*" -exec rm -rf {} \;
    find: ‘/tmp/vmware-root_560-2957190359’: 没有那个文件或目录
    find: ‘/tmp/vmware-root_555-4282367637’: 没有那个文件或目录
    find: ‘/tmp/vmware-root_631-4021718894’: 没有那个文件或目录
   [root@localhost tmp]# ls
   ks-script-ed2ODG
   nginx_kaku.tar.gz
   systemd-private-d38b668730bf4589896221daead5dbea-chronyd.service-be3NkF
   yum.log
find /root -type f -mmin -30 ! -name ".*"  -exec rm {} \;
find /root  -maxdepth 1  -type d  -name "Apa*"   -mmin -30 -exec cp -a {} /tmp 
\; # 复制到tmp目录中
```

### su(切换用户)

```shell
su全称：switch user
# root用户可以很方便的切换到任意用户
[root@localhost ~]# su - kaku
上一次登录：一 3月 27 15:03:29 CST 2023从 192.168.2.110pts/1 上
[kaku@localhost ~]$ ls
kaku kaku2 kaku2.txt kaku.txt
[kaku@localhost ~]$ exit # 退出，又回到root用户了
登出
[root@localhost ~]# 
# 普通用户切换到root用户，必须输入root密码
[kaku@localhost ~]$ su - root
密码：  # 需要输入root用户的密码
上一次登录：一 3月 27 10:48:24 CST 2023从 192.168.2.110pts/0 上
[root@localhost ~]# exit
登出
[kaku@localhost ~]$ 
# 不带-也是可以的，带-的话，就是切换完用户之后，直接到用户家目录下，不带-就不是家目录。
[kaku@localhost ~]$ su root
密码：
[root@localhost kaku]# exit
```

### sudo(提升权限)

```shell
# sudo全称：superuser do，它的作用是用来授权的。就是给普通用户高级权限用的。原因就是很多的操作，如果都需要root用户去做，太麻烦了，所以可以给普通用户做一些授权，普通用户操作就方便了。授权就用到了sudo，sudo并不是一下子给用户很多权限，而是一个命令一个命令的授权。
# sudo需要修改配置才能开启。
# root用户才能修改这个配置。
1.配置/etc/sudoers
# 直接visudo就能编辑这个文件
[root@localhost ~]# visudo
#用户名   所有终端 = 运行的用户身份   命令ALL，ALL是所有指令，不能给所有的，不然权限太高了
#在100行下面添加如下内容
kaku  ALL=(ALL)       /bin/systemctl,/usr/bin/vim,/usr/sbin/reboot   # 单独给指令权限，而且要写指令的绝对路径，逗号分割
# 修改完配置文件，保存退出之后，立马就生效了，不需要重启或者重新登录。
#切换到普通用户，查看可以使用的授权命令
sudo -l
[kaku@localhost ~]$ sudo -l
我们信任您已经从系统管理员那里了解了日常注意事项。
总结起来无外乎这三点：
    #1) 尊重别人的隐私。
    #2) 输入前要先考虑(后果和风险)。
    #3) 权力越大，责任越大。
[sudo] kaku 的密码： # 需要输入kaku用户的密码
匹配 %2$s 上 %1$s 的默认条目：
   !visiblepw, always_set_home, match_group_by_gid, always_query_group_plugin, 
env_reset,
    env_keep="COLORS DISPLAY HOSTNAME HISTSIZE KDEDIR LS_COLORS", 
env_keep+="MAIL PS1 PS2 QTDIR USERNAME
   LANG LC_ADDRESS LC_CTYPE", env_keep+="LC_COLLATE LC_IDENTIFICATION 
LC_MEASUREMENT LC_MESSAGES",
   env_keep+="LC_MONETARY LC_NAME LC_NUMERIC LC_PAPER LC_TELEPHONE", 
env_keep+="LC_TIME LC_ALL LANGUAGE
LINGUAS _XKB_CHARSET XAUTHORITY", 
secure_path=/sbin\:/bin\:/usr/sbin\:/usr/bin
用户 kaku 可以在 localhost 上运行以下命令： # 提示可以使用sudo来执行的命令
   (ALL) /bin/systemctl, /usr/bin/vim, /usr/sbin/reboot
[kaku@localhost ~]$
2.使用sudo执行命令
# 授权的命令使用起来和普通指令是不同的，需要使用sudo来执行命令，也就是以授权的方式来执行指令。
# 比如reboot重启
[kaku@localhost ~]$ sudo reboot
Connection closing...Socket close.
Connection closed by foreign host.
...
# 比如重启网卡
# sudo systemctl restart network   #start,stop,restart
# 比如：vim权限
[kaku@localhost ~]$ vim /etc/shadow
[kaku@localhost ~]$ sudo vim /etc/shadow 
# 注意，vim的权限很大，比如可以修改密码，可以修改授权配置文件等，甚至root用户的密码都可以修改，所以不要将vim的root权限给普通用户。
```



## 用户和用户组管理

### useradd(创建用户)

```shell
#创建用户
useradd 
#创建一个用户
例子1：useradd test1
```

### passwd(设置用户密码)

```shell
#设置密码，远程ssh连接是需要密码的，所以想让某个用户登录系统，必须设置密码
passwd
例子1：passwd test1
#用root用户给普通用户修改密码
[root@localhost ~]# passwd test1
更改用户 test1 的密码 。
新的 密码：123456
无效的密码： 密码是一个回文
重新输入新的 密码：123456
passwd：所有的身份验证令牌已经成功更新。

#普通用户自[test1@localhost ~]$ passwd  # 给当前登录用户修改密码，root用户修改密码不需要输入旧密码，普通用户需要输入旧密码
更改用户 test1 的密码 。
（当前）UNIX 密码：
新的 密码：
无效的密码： 密码少于 8 个字符
新的 密码：
无效的密码： 密码少于 8 个字符
新的 密码：
无效的密码： 密码未通过字典检查 - 过于简单化/系统化
passwd: 已经超出服务重试的最多次数
# 一般linux的密码是有复杂度要求的，比如下面这种密码就可以通过：大小写组合、数字、特殊字符组合起来超过8位。
例子3：
#免交互修改密码，这样不需要输入两次密码确认。echo是打印的意思，有结果输出给passwd命令来修改test1用户的密码
echo 123456|passwd --stdin test1
# 这种一般同时改多个Linux服务器系统的密码时比较方便。己修改密码
[test1@localhost ~]$ passwd  # 给当前登录用户修改密码，root用户修改密码不需要输入旧密码，普通用户需要输入旧密码
更改用户 test1 的密码。
为 test1 更改 STRESS 密码。
（当前）UNIX 密码：
新的 密码：
无效的密码： 密码少于 8 个字符
新的 密码：
无效的密码： 密码少于 8 个字符
新的 密码：
无效的密码： 密码未通过字典检查 - 过于简单化/系统化
passwd: 已经超出服务重试的最多次数
# 一般linux的密码是有复杂度要求的，比如下面这种密码就可以通过：大小写组合、数字、特殊字符组合起来超过8位。
aabbcc123/
例子3：
#免交互修改密码，这样不需要输入两次密码确认。echo是打印的意思，有结果输出给passwd命令来修改test1用户的密码
echo 123456|passwd --stdin test1
# 这种一般同时改多个Linux服务器系统的密码时比较方便。
```

### id(查看用户uid和所属组)

```shell
例子1: 
#用户存在，系统的返回结果
[root@localhost ~]# id test1
uid=1000(test1) gid=1000(test1) 组=1000(test1)
#用户不存在，系统的返回结果
[root@localhost ~]# id test2
id: test2: no such user
```

### userdel(删除用户)

```shell
例子1：
#被删除的用户还在登录状态，是不能删除的
[root@localhost ~]# userdel test1
userdel: user test1 is currently used by process 2356
#被删除的用户，退出登录之后，可以正常删除
[root@localhost ~]# userdel test1
linux删除用户之后，/home/目录下对应的用户文件夹还在，如果还想加回来这个用户，那么会提示家目录存在，不会从样板目录(skel)中复制任何文件了，通过ls -a /etc/skel，可以看到skel目录下的内容了。还提示邮箱文件已经存在，ls /var/spool/mail下面
windows删除用户之后，c:\Users目录下的用户文件夹也还在
注意：删除之后的用户，再次创建出来，密码是需要重新设置的
[root@localhost ~]# userdel -r test1 # 删除用户，并删除用户相关所有目录
```

### usermod(修改用户信息)

```shell
#修改用户信息，修改属性
usermod # modify 它有很多选项(参数)，-L是锁定用户，通过命令 -h(或者--help，一个-后面一般跟一个字母即可，两个-后面一般跟完整单词)，可以查看命令的各种选项的意思，比如usermod -h
#锁定用户(和windows的禁用用户一个意思)
例子1：
[root@localhost ~]# usermod -L test1 #被锁定的用户，下次就登录不上系统了。
[root@localhost ~]# usermod -U test1 #解锁用户
[root@localhost ~]# lchage -l test1 # 查看用户详细信息
帐号被锁。
至少: 0
至多: 99999
警告: 7
不活跃： 从不
最后一次改变： 2021年07月20日
密码过期： 从不
密码不活跃： 从不
帐号过期： 从不
#禁止用户登录
[root@localhost ~]# usermod -s /sbin/nologin test2
[root@localhost ~]# grep -w 'test2' /etc/passwd
test2:x:1001:1001::/home/test2:/sbin/nologin

# 修改用户所属的主组
usermod -g 组名
例子：
[root@localhost tmp]# usermod -g test test1 #将test1用户的主组改为test

# 将用户添加到多个其他组中
usermod -G
[root@localhost tmp]# usermod -G test2 test1 # 将test1用户也添加到test2组
```

### lchange(查看用户详细信息)

```shell
#查看用户详细信息
lchage
例子1：
[root@localhost ~]# lchage -l test1
帐号没被锁。
至少: 0
至多: 99999
警告: 7
不活跃： 从不
最后一次改变： 2021年07月20日
密码过期： 从不
密码不活跃： 从不
帐号过期： 从不
```

```shell
所有的用户信息存储在/etc/passwd文件中，每创建一个用户该文件就会多一行记录
test1:x:1000:1000::/home/test1:/bin/bash
第一列：用户名
第二列：x
第三列：uid  # root用户的uid是0，我们自己创建的用户uid是1000及之后的数值。
第四列：gid
第五列：注释，一般为空
第六列：家目录的位置
第七列：使用shell的名称，默认使用/bin/bash

所有的用户密码信息存储/etc/shadow，设置了密码的长度比较长。密码是两层加密的，基本无法破解。但是如果黑客权限比较高，它可以用知道密码的shadow文件来替换这个文件，或者修改这个文件下某个用户的密码，只有root用户才有权力修改这个文件。
```

### w(查看当前登录了几个用户)

```shell
w
结果：下面表示2个终端登录了
12:15:42 up 21 min,  2 users, load average: 0.00, 0.01, 0.03
USER     TTY     FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
root     tty1                      12:15    6.00s  0.00s  0.00s -bash
root     pts/0    192.168.61.1     11:55    6.00s  0.02s  0.01s w
# tty1表示本地登录的、pts/0表示远程登录的
```

## 用户组管理

### group(新建组)

```shell
新建组和查看组:
 groupadd 组名
例子：
 [root@localhost tmp]# groupadd test
 [root@localhost tmp]# cat /etc/group # 查看有哪些组
 
# 指定组来创建用户，如果没有指定组，那么创建用户的时候，linux会自动创建一个与用户名同名的组。
例子： 组的英文是group
[root@localhost tmp]# useradd -g test1 test3 #-g 是指定主组
[root@localhost tmp]# id test3
uid=1002(test3) gid=1000(test1) 组=1000(test1)
gid表示用户的属组的主组
组=表示用户的属组，用户可以属于多个组，一个主组，多个其他组。
```

### groupdel(删除组)

```shell
# 删除组
groupdel 组名
例子：
[root@localhost tmp]# groupdel test #如果组内有用户，会报错，需要先删除主组属于这个组的所有用户(userdel -r 用户名)，或者将用户移到其他的组之后在删除组。
# 修改组名
groupmod -n test1 test2 # 将test2组名改为test1
```

## 权限管理

root用户权限最高，所以一般对他不做什么权限设置。其他用户就要设定权限并且遵守权限了。

### 文件权限

```shell
#文件属性
[root@localhost ~]# ls -l /tmp/123.txt
-rw-r--r--. 1 root root 08月 09 21:17 /tmp/123.txt
#第一段的第一个字符，表示文件类型 -文件、d目录、l软链接(对应着windows快捷方式)、b块设备(ls /dev，可以看到硬盘sda等)
#第一段第2-4字符，表示该文件所属用户的权限
#第一段第5-7字符，表示该文件所属用户组的权限
#第一段第8-10字符，表示其他用户对该文件的权限
r 4 代表读权限 read
w 2 代表写权限 write
x 1 代表可执行权限 executable  
- 0 空权限位，表示没有这个权限，9位权限不能少，没有的权限就用-代替。
权限值表
0 ---
1 --x
2 -w-
3 -wx
4 r--
5 r-x
6 rw-
7 rwx
ugo权限体系:
   rw-   r--   r-- 
   user group other
```

### chmod(修改文件和目录权限)

```shell
# 例如：chomd -r,就是去掉r权限，chomd +r就是加上读权限，chmod +wr就是加读写权限，chmod u+r，就是给文件属主用户添加读权限等
[lisi@localhost ~]$ touch 1.txt
[lisi@localhost ~]$ vi 1.txt
[lisi@localhost ~]$ ls -l
总用量 4
-rw-rw-r--. 1 lisi lisi 08月 09 21:17 1.txt
[lisi@localhost ~]$ chmod -rw 1.txt 
[lisi@localhost ~]$ ls -l
总用量 4
----------. 1 lisi lisi 08月 09 21:17 1.txt
# 现在这个文件是没有任何权限的，但是文件是lisi创建的，文件属主还是lisi，虽然显示lisi也没有权限，但是实际上lisi是可以修改文件权限的，其他用户(除了root)是没有权力修改这个文件权限的。

# 如果我们想将某个文件的：rwxr-xr-x权限改为--x-w-r--，如果按照前面我们chmod指定字母的形式来修改，就比较麻烦，直接使用权限对应的数字改就很方便：
rwxr-xr-x 对应的值为：755
--x-w-r-- 对应的值为：124
[lisi@localhost tmp]$ chmod 124 1.txt
[lisi@localhost tmp]$ ls -l
总用量 144
---x-w-r--. 1 lisi   lisi       25 3月  20 09:24 1.txt

#改变文件的权限，例如：chomd -r,就是去掉r权限，chomd +r就是加上读权限
chmod
例子1：
#修改权限之前
[test1@localhost tmp]$ ls -l
总用量 4
-rw-rw----. 1 test1 test1 8 7月  20 17:20 test1.txt
#修改权限
[test1@localhost tmp]$ chmod u+x test1.txt 
#修改权限之后
[test1@localhost tmp]$ ls -l
总用量 4
-rwxrw----. 1 test1 test1 8 7月  20 17:20 test1.txt
例子2：
同时修改多个权限
[test1@localhost tmp]$ chmod u-x,g-x,o+x test1.txt 
[test1@localhost tmp]$ ls -l
总用量 4
-rw-rw---x. 1 test1 test1 8 7月  20 17:20 test1.txt
例子3：数字修改更方便
[test1@localhost tmp]$ chmod 777 test1.txt 
[test1@localhost tmp]$ ls -l
总用量 4
-rwxrwxrwx. 1 test1 test1 8 7月  20 17:20 test1.txt
```

### 读权限的作用

```shell
lisi用户：
   [lisi@localhost ~]$ chmod -rw 1.txt 
   [lisi@localhost ~]$ ls -l
   总用量 4
    ----------. 1 lisi lisi 12 3月  20 09:07 1.txt
   [lisi@localhost ~]$ cat 1.txt
    cat: 1.txt: 权限不够
   [lisi@localhost ~]$ chmod u+r 1.txt
   [lisi@localhost ~]$ ls -l
   总用量 4
    -r--------. 1 lisi lisi 12 3月  20 09:07 1.txt
   [lisi@localhost ~]$ cat 1.txt
   hello kaku1
   为了方便其他用户查看，我们先将1.txt放到/tmp目录下。
   [lisi@localhost ~]$ mv 1.txt /tmp/
   [lisi@localhost ~]$ ls /tmp/
    1.txt          
wangwu用户：
 [wangwu@localhost ~]$ cd /tmp/
 [wangwu@localhost tmp]$ cat 1.txt
 cat: 1.txt: 权限不够
 [wangwu@localhost tmp]$ chmod o+r 1.txt
 chmod: 更改"1.txt" 的权限: 不允许的操作
切换到lisi：给o加上r权限，再看效果
 [lisi@localhost ~]$ chmod o+r /tmp/1.txt
 [lisi@localhost ~]$ ls -l /tmp/
   总用量 8
    -r-----r--. 1 lisi lisi  12 3月  20 09:07 1.txt
再切换到wangwu来查看文件内容：
 [wangwu@localhost tmp]$ cat 1.txt
 hello kaku
```

### 写权限的作用

```shell
但是wangwu想编辑文件，也是没有权限的。可以vi打开，但是编辑之后不能保存。
再切换到lisi，给o一个w权限，wangwu就可以编辑保存了。 
 [lisi@localhost ~]$ chmod o+w /tmp/1.txt
 [lisi@localhost ~]$ ls -l /tmp/
 总用量 8
 -r-----rw-. 1 lisi lisi  12 3月  20 09:07 1.txt
wangwu编辑保存一下，查看内容：
 [wangwu@localhost tmp]$ vi 1.txt
 [wangwu@localhost tmp]$ cat 1.txt
 hello kaku
 hello wangwu
```

### 可执行权限的作用

```sehll
这个需要我们创建一个命令文件才能看效果，我复制某个命令文件过来，谁复制过来的，这个文件的属主就是谁，如下
[lisi@localhost ~]$ cd /tmp/
[lisi@localhost tmp]$ cp /bin/ls .
[lisi@localhost tmp]$ ls -l
   总用量 124
    -r-----rw-. 1 lisi lisi     25 3月  20 09:24 1.txt
    -rwx------. 1 root root    836 3月  15 20:14 ks-script-ed2ODG
    -rwxr-xr-x. 1 lisi lisi 117608 3月  20 09:29 ls
   [lisi@localhost tmp]$ chmod -x ls
   [lisi@localhost tmp]$ ls -l
   总用量 124
    -r-----rw-. 1 lisi lisi     25 3月  20 09:24 1.txt
    -rwx------. 1 root root    836 3月  15 20:14 ks-script-ed2ODG
    -rw-r--r--. 1 lisi lisi 117608 3月  20 09:29 ls
切换到wangwu来执行一下ls这个文件： 注意，不能直接ls，直接ls还是调用系统/bin/ls文件，需要
写./ls才是使用当前目录下的ls文件，或者写这个文件的绝对路径/tmp/ls，或者将它放到某个特定目录
下，就可以直接使用对应指令而不用管路径了，这个我在下面有补充说明。
 [wangwu@localhost tmp]$ ./ls
 -bash: ./ls: 权限不够
 [wangwu@localhost tmp]$ /tmp/ls
 -bash: /tmp/ls: 权限不够
```

### 可执行程序特殊目录说明

```shell
通过echo $PATH可以看到，类似于windows的环境变量中的PATH。反式放到这个目录中的命令程序，我们可以在任意目录下通过这个命令程序名称来直接调用命令来执行：
[lisi@localhost tmp]$ echo $PATH  # 下面这几个就是环境变量路径存放位置
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/lisi/.local/bin:/home/lisi/bin
lisi@localhost tmp]$ cp ./ls /home/lisi/bin/
[lisi@localhost tmp]$ ls /home/lisi/bin/
ls
[lisi@localhost tmp]$ mv /home/lisi/bin/ls /home/lisi/bin/xxx  # 为了不和系统默认的
ls冲突，我们改名为xxx
[lisi@localhost tmp]$ ls /home/lisi/bin/
xxx
[lisi@localhost tmp]$ xxx
[lisi@localhost tmp]$ xxx  # 命令可以在任意目录下直接执行
1.txt 			vmware-root_552-2957583561
ls
```

### chown(修改文件所属)

```shell
chown，全称Change Owner，改变拥有者。
#修改文件的所属,普通用户是不能修改其他用户文件的所属的，需要root用户，所以先切换到root用户来操
作
chown
例子1：修改所属用户和用户组，test2:test2，前面的test2表示用户，后面的test2是组
[root@localhost tmp]# chown test2:test2 ls
[root@localhost tmp]# ls -l
总用量 404
-rwxr-xr-x. 1 test2 test2 159024 7月  20 17:43 grep
-rwxr-xr-x. 1 test2 test2 117608 7月  20 17:38 ls
-rwxr-xr-x. 1 test1 test1 130360 7月  20 17:43 mv
-rw-rw-rw-. 1 test1 test1     14 7月  20 17:38 test1.txt
# 修改所属用户
[root@localhost tmp]# chown test1 ls
[root@localhost tmp]# ls -l
总用量 404
-rwxr-xr-x. 1 test2 test2 159024 7月  20 17:43 grep
-rwxr-xr-x. 1 test1 test2 117608 7月  20 17:38 ls
-rwxr-xr-x. 1 test1 test1 130360 7月  20 17:43 mv
-rw-rw-rw-. 1 test1 test1     14 7月  20 17:38 test1.txt
```

### 目录权限

```shell
# 修改目录权限和所属
例子3：文件夹(目录权限)
用root用户创建一个文件夹，文件夹默认所属用户和组为root:root，那么普通用户是没全限制在这个目录
中创建文件的。
[root@localhost ~]# cd /tmp/
[root@localhost tmp]# mkdir kaku
[root@localhost tmp]# ls -l
drwxr-xr-x. 2 root   root        6 3月  20 11:36 kaku
普通用户，比如lisi想在里面创建文件：
[lisi@localhost tmp]$ cd kaku/
[lisi@localhost kaku]$ touch 2.txt
touch: 无法创建"2.txt": 权限不够
如何让lisi有创建文件的权限呢？创建文件的权限就是目录写权限
首先要切换到root用户，然后用root用户修改目录权限，或者直接将目录的所属修改为lisi
修改权限：
   [root@localhost tmp]# chmod o+w kaku
   [root@localhost tmp]# ls -l
   drwxr-xrwx. 2 root   root        6 3月  20 11:36 kaku
切换到lisi，创建文件：
 [lisi@localhost kaku]$ touch 2.txt
   [lisi@localhost kaku]$ ls
    2.txt
修改所属：
 [root@localhost tmp]# chmod o-w kaku
 [root@localhost tmp]# ls -l
 drwxr-xr-x. 2 root   root       19 3月  20 11:39 kaku
 [root@localhost tmp]# chown lisi:lisi kaku
 [root@localhost tmp]# ls -l
 drwxr-xr-x. 2 lisi   lisi       19 3月  20 11:39 kaku
切换到lisi： 
 [lisi@localhost kaku]$ touch 3.txt
   [lisi@localhost kaku]$ ls
    2.txt  3.txt
lisi也可以修改目录的权限了，因为它完全属于的lisi：
 [lisi@localhost tmp]$ chmod o+w kaku
 [lisi@localhost tmp]$ ls -l
 drwxr-xrwx. 2 lisi   lisi       32 3月  20 11:42 kaku
#使用uid和gid修改文件的所属用户和所属用户组 属主，属组
例子2：
[root@localhost tmp]# ls -l
总用量 404
-rwxr-xr-x. 1 test2 test2 159024 7月  20 17:43 grep
-rwxr-xr-x. 1 test1 test2 117608 7月  20 17:38 ls
-rwxr-xr-x. 1 test1 test1 130360 7月  20 17:43 mv
-rw-rw-rw-. 1 test1 test1     14 7月  20 17:38 test1.txt
[root@localhost tmp]# id test1
uid=1000(test1) gid=1000(test1) 组=1000(test1)
[root@localhost tmp]# id test2
uid=1001(test2) gid=1001(test2) 组=1001(test2)
[root@localhost tmp]# useradd -g test1 test3
[root@localhost tmp]# id test3
文件权限和目录权限的解释说明：
6、文件属性详解
uid=1002(test3) gid=1000(test1) 组=1000(test1)
[root@localhost tmp]# chown 1001:1001 test1.txt 
[root@localhost tmp]# ls -l 
总用量 404
-rwxr-xr-x. 1 test2 test2 159024 7月  20 17:43 grep
-rwxr-xr-x. 1 test1 test2 117608 7月  20 17:38 ls
-rwxr-xr-x. 1 test1 test1 130360 7月  20 17:43 mv
-rw-rw-rw-. 1 test2 test2     14 7月  20 17:38 test1.txt
```

```shell
文件权限和目录权限的解释说明:
文件权限： rwx 读写执行
目录的权限： rwx，r表示可以查看目录下有哪些文件 w表示可以在目录中创建、修改、删除文件等操作 x表示可以cd切换到该目录
为了安全操作：
文件权限默认： 644权限、狠一点就给600权限
目录权限默认： 755权限、狠一点就给700权限
```

### 文件属性详解

```shell
#文件属性
[root@localhost ~]# ls -l 
-rw-rw-rw-. 1 lisi   lisi     0 3月  20 16:00 222.txt
#第一段的第一个字符，表示文件类型 -文件、d目录、l软链接(对应着windows快捷方式)、b块设备(ls /dev，可以看到硬盘sda等)
#第一段第2-4字符，表示该文件所属用户的权限
#第一段第5-7字符，表示该文件所属用户组的权限
#第一段第8-10字符，表示其他用户对该文件的权限
#第一段的第11个字符. ，表示开启selinux的状态下创建的，也证明selinux是开启状态的。
# 看到.表示这个文件受到selinux的保护，selinux：https://baike.baidu.com/item/SELinux/8865268?fr=aladdin，这个东西很安全，但是有了它变得很麻烦，安全和便利一般是冲突的。主要是红帽系的系统(redhat\centos\阿里的龙蜥\华为的欧拉)有这个机制。我们一般上来就是关闭它，安全方面我们通过其他方法来控制。查看selinux的指令：
 # 查看状态
 [lisi@localhost tmp]$ sestatus
   SELinux status:                 enabled  # enabled表示开启状态，disabled表示禁用
状态
   SELinuxfs mount:               /sys/fs/selinux
   SELinux root directory:         /etc/selinux
   Loaded policy name:             targeted
   Current mode:                   enforcing
   Mode from config file:         enforcing
   Policy MLS status:             enabled
   Policy deny_unknown status:     allowed
   Max kernel policy version:      31
 # 关闭和开启selinux，需要root权限才能修改
 [root@localhost tmp]# ls -l /etc/selinux/config 
 -rw-r--r--. 1 root root 543 3月  15 20:11 /etc/selinux/config
 [root@localhost tmp]# vi /etc/selinux/config 
 把7行改为： SELINUX=disabled  #然后保存退出，并且重启系统才会生效。
 # 然后再登录创建文件，查看文件信息，就看不到.了
 [root@localhost ~]# touch 1.txt
  [root@localhost ~]# ls -l
   总用量 16
    -rw-r--r--  1 root root    0 3月  20 13:32 1.txt
#第二段的数字，表示该文件的硬链接数量，ln是创建硬链接的指令。
#第三段的字符串，表示该文件所属用户
#第四段的字符串，表示该文件所属用户组
#第五段的数字，表示该文件的大小，默认单位为B，如果想按照KB来显示，那么可以通过ls -lh指令来查看。h是human的意思，以人类可读的方式显示，会自动按照文件大小来设定显示单位。
#第六段到倒数第二段，都是该文件的修改时间，只要改动了文件内容，这个时间就会自动变为修改文件时的时
间。
 #其实linux系统会记录三个时间：
 # 访问时间(access time) 文件被打开时自动变化这个时间
 # 修改时间(modify time) 文件内容发生变化时自动改变这个时间，ls -l 显示的就是这个时
间。
 # 改变时间(change time) 文件属性发生变化时自动改变这个时间，文件大小也是文件的属性，所以修改文件内容导致大小变化的时候，这个时间也会自动改变。
 #windows系统也会记录三个时间：访问时间、创建时间、修改时间
 #linux下通过stat指令来查看：
 [root@localhost ~]# stat 1.txt
         文件："1.txt"
         大小：0         块：0         IO 块：4096   普通空文件
       设备：801h/2049d Inode：67108933   硬链接：1
       权限：(0644/-rw-r--r--) Uid：(    0/   root)   Gid：(    0/   root)
       最近访问：2023-03-20 13:32:34.333042228 +0800
       最近更改：2023-03-20 13:32:34.333042228 +0800
       最近改动：2023-03-20 13:32:34.333042228 +0800
       创建时间：-
 # 我们改一下文件权限，然后再看时间
   [root@localhost ~]# chmod 777 1.txt
       [root@localhost ~]# stat 1.txt
         文件："1.txt"
         大小：0         块：0         IO 块：4096   普通空文件
       设备：801h/2049d Inode：67108933   硬链接：1
       权限：(0777/-rwxrwxrwx) Uid：(    0/   root)   Gid：(    0/   root)
       最近访问：2023-03-20 13:32:34.333042228 +0800
       最近更改：2023-03-20 13:32:34.333042228 +0800
       最近改动：2023-03-20 13:56:43.005634151 +0800  # 改动时间变了
       创建时间：-
#最一段，该文件的名称
```

## shell提示符

```shell
#root用户提示符
[root@localhost ~]# 
#普通用户test1的提示符
[test1@localhost ~]$ 
#格式：
[用户名@主机名 所在目录]#
# 1、用户名，这个没说啥说的
# 2、主机名：localhost是主机名，windows电脑也有主机名：我的电脑-->属性-->高级系统设置-->计
算机名，同一个网络中如果有多台计算机的话，每个计算机都应该有个自己的名字，就是主机名。Linux主机
名默认叫做localhost，也是可以修改的
   [root@localhost ~]# hostname kaku
   [root@localhost ~]# logout
   退出之后，在重新登录，就看到主机名改好了，如下
   [root@kaku ~]hostname
   kaku
# 3、所在目录：root登录之后，默认所在目录是/root，此时~表示的/root目录，如果是普通用户登录
的，那么~表示的是用户家目录，cd切换目录的时候，显示的当前所在目录
    # root用户：
   [root@kaku ~]# pwd
   /root
 # 普通用户：
   [zhangsan@kaku ~]$ pwd
 /home/zhangsan
# 4、提示符号
 #代表当前登录的用户是管理员,$代表的是当前登录用户是普通用户
#提示符格式定制，这个简单理解一下即可，一般都不改
# 原格式：
[root@test ~] echo $PS1
[\u@\h \W]\$   # \u是用户，\h是主机名，\W是相对路径
# 临时修改：重新登录就又还原了
[root@test bin]export PS1='[\u@\h \w]\$' # \w表示绝对路径
#永久修改
[root@test 10:24:25 ~]vi .bashrc 
#找个空白的地方，插入一行
export  PS1='[\u@\h \t \w]\$'
#linux PS1可以各种定制：参考https://www.cnblogs.com/Q--T/p/5394993.html
```

## 终端常用快捷键

```shell
Ctrl + a    #光标跳转至正在输入的命令行的首部
Ctrl + e    #光标跳转至正在输入的命令行的尾部
Ctrl + c    #终止前台运行的程序，比如ping指令
Ctrl + d    #在shell中，ctrl-d表示推出当前shell。
Ctrl + z    #将任务暂停，挂至后台, 执行fg命令继续运行
Ctrl + l    #清屏，和clear命令等效。
Ctrl + k    #删除从光标到行末的所有字符
Ctrl + u    #删除从光标到行首的所有字符
Ctrl + r    #搜索历史命令, 利用关键字搜索
ctrl + w    #光标往前删除一个参数，以空格为分割。
```

## alias(命令别名)

```shell
#别名
alias
# 比如：ls -l 直接可以写ll即可
例子1：
#查看别名
[root@test 15:23:17 ~]#alias 
alias cp='cp -i'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l.='ls -d .* --color=auto'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
alias mv='mv -i'
alias rm='rm -i'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --showtilde'
例子2：
#添加别名
[test1@test 15:24:23 ~]$alias rm='rm -i'  # -i是提示警告信息用的
[test1@test 15:27:08 ~]$alias |grep rm
alias rm='rm -i'
或者：[test1@test 15:24:23 ~]$alias rm='echo 禁止使用删除操作'
例子3：
#取消别名
[test1@test 15:27:13 ~]$unalias ls
[test1@test 15:27:47 ~]$alias |grep ls
alias别名的优先级高于系统命令
别名一定要是可执行的，不能随便定义别名，比如kaku='aaaaaaa'，执行kaku会报错，没有aaaaaaa这
个指令
例子4：
#alias永久生效
[root@localhost ~]# vi .bashrc 
#空白处，增加一行
alias cip='ip addr|tail -4|head -1'
```

## 输入输出重定向

输入输出只能对文件进行操作，不能对目录操作。

### 输出重定向

```shell
输出：
   > 输出重定向， 将命令执行结果不输出到屏幕上，输出到文件里，会清空原文件，所以输出的时候一定要注意，文件名称要看好了。
       [root@localhost ~]# head -20 services > 2.txt
       [root@localhost ~]# seq 100 > 1.txt
       [root@localhost ~]# echo 123 > 1.txt
       [root@localhost ~]# > 1.txt # 清空文件内容
       
  >> 输出追加重定向，不会清空原文件
       [root@localhost ~]# echo aaaaa >> 2.txt
       
#标准正确输出重定向1
#标准错误输出重定向2
       [root@localhost ~]# cat kaku.txt 
       hello kaku 
       what are you nongshalie!
       [root@localhost ~]# cat kakuu # 错误信息默认是打印在屏幕上的，如果我们想记录错误信息，就可以用到标准错误输出
        cat: kakuu: 没有那个文件或目录
       [root@localhost ~]# cat kaku.txt 1>1.txt 2>2.txt # 指令正确会将数据保存到1.txt中
       [root@localhost ~]# cat 1.txt
       hello kaku 
       what are you nongshalie!
       [root@localhost ~]# cat 2.txt
       [root@localhost ~]# cat kakuu 1>1.txt 2>2.txt #kakuu文件不存在，报错信息会进入到2.txt中
       [root@localhost ~]# cat 1.txt
       [root@localhost ~]# cat 2.txt # 记录了报错信息
        cat: kakuu: 没有那个文件或目录
```

### 输入重定向

```shell
输入：
   < 输入重定向
   [root@localhost ~]# cat < kaku.txt > 3.txt # kaku.txt的数据输入过来并写
入3.txt中
   << 输入追加重定向
    # 标准输入0，支持用户直接输入内容
   [root@localhost ~]# cat << 0
       > 1
       > 2
       > 2222
       > 0
        1
        2
        2222
       [root@localhost ~]# cat << 0 > 22.txt
       > a
       > b
       > ddd
       > 0
       [root@localhost ~]# cat 22.txt
       a
       b
       ddd
```

## Linux压缩打包

### tar

```shell
# 压缩文件有时候我们也叫做归档文件。但是归档和压缩有一些区别，归档只是将多个文件捆绑成一个文件，并没有压缩，而压缩才是将大小压缩的更小。
#Linux最常用的压缩和解压指令是：
tar：能够解压的文件格式是xx.tar.gz
 压缩：tar -zcf 压缩包路径 目标1 目标2 目标3 ...
 解压：tar -zxf 解压路径
例子1：压缩和解压文件
[root@localhost ~]# ls
123.txt  4.txt           a.txt c.txt         kaku.txt
1.txt   anaconda-ks.cfg b.txt kaku.tar.gz services
[root@localhost ~]# rm -f *
[root@localhost ~]# ls
[root@localhost ~]# cp /etc/services .
[root@localhost ~]# tar -zcf kaku.tar.gz services #压缩文件
[root@localhost ~]# ls
kaku.tar.gz services 
[root@localhost ~]# ls -lh
-rw-r--r--  1 root root 134K 3月  22 14:51 kaku.tar.gz
-rw-r--r--  1 root root 655K 3月  22 11:22 services
[root@localhost ~]# rm -f services # 删除原文件之后就再解压
[root@localhost ~]# tar -zxf kaku.tar.gz   # 解压文件
[root@localhost ~]# ls -lh
-rw-r--r--  1 root root 134K 3月  22 14:51 kaku.tar.gz
-rw-r--r--  1 root root 655K 3月  22 11:22 services  #看到和源文件一样的文件，包括文件
属性也一样。
例子2：
#归档，但是不压缩
tar -cf
[root@localhost ~]# cp /etc/services ./shike # 再拷贝一个services文件过来
[root@localhost ~]# ls -lh
总用量 14M
-rw-r--r-- 1 root root 13M 3月  22 14:58 2.tar.gz
-rw-r--r-- 1 root root 134K 3月  22 14:56 kaku.tar.gz
-rw-r--r-- 1 root root 655K 3月  22 14:55 services
-rw-r--r-- 1 root root 655K 3月  22 15:04 shike
[root@localhost ~]# tar -cf 3.tar.gz services shike #归档，但是不压缩
linux系统下解压文件的时候，不同格式的压缩包需要使用不同的命令来解压或者压缩。
2、gzip
[root@localhost ~]# ls -lh
总用量 15M
-rw-r--r-- 1 root root 13M 3月  22 14:58 2.tar.gz
-rw-r--r-- 1 root root 1.3M 3月  22 15:04 3.tar.gz  #看大小就知道没有压缩大小。
-rw-r--r-- 1 root root 134K 3月  22 14:56 kaku.tar.gz
-rw-r--r-- 1 root root 655K 3月  22 14:55 services
-rw-r--r-- 1 root root 655K 3月  22 15:04 shike
例子3：
#查看压缩包内容
[root@localhost ~]# tar -tf 3.tar.gz 
services
shike
tar这个指令的参数可以不加-，比如tar tf 3.tar.gz
```

linux系统下解压文件的时候，不同格式的压缩包需要使用不同的命令来解压或者压缩。

### gzip

```shell
#压缩文件，会自动删除原文件，和tar不同，tar会留着原文件
[root@localhost ~]# gzip services 
[root@localhost ~]# ls -lh
总用量 15M
-rw-r--r-- 1 root root 133K 3月  22 14:55 services.gz
-rw-r--r-- 1 root root 655K 3月  22 15:04 shike
# 解压，会自动删除原压缩包
[root@localhost ~]# gzip -d services.gz 
[root@localhost ~]# ls -lh
总用量 16M
-rw-r--r-- 1 root root 655K 3月  22 14:55 services
-rw-r--r-- 1 root root 655K 3月  22 15:04 shike
#压缩多个文件，每一个文件产生一个单独的压缩包
[root@localhost ~]# gzip services shike 
[root@localhost ~]# ls -lh
总用量 15M
-rw-r--r-- 1 root root 133K 3月  22 14:55 services.gz
-rw-r--r-- 1 root root 133K 3月  22 15:04 shike.gz
#解压缩
[root@localhost ~]# gzip -d services.gz shike.gz 
[root@localhost ~]# ls -lh
总用量 16M
-rw-r--r-- 1 root root 655K 3月  22 14:55 services
-rw-r--r-- 1 root root 655K 3月  22 15:04 shike
gzip其实感觉并不太好用，但是工作中我们可能会遇到gzip的压缩包。
```

### zip

```shell
#压缩
zip
例子1：
# -r会递归压缩 directory 目录及其子目录中的所有文件，并保留目录结构。
[root@localhost ~]# zip -r 1.zip services shike #会保留原文件
 adding: services (deflated 80%)
 adding: shike (deflated 80%)
[root@localhost ~]# ls -lh
总用量 16M
-rw-r--r-- 1 root root 267K 3月  22 15:25 1.zip
-rw-r--r-- 1 root root 655K 3月  22 14:55 services
-rw-r--r-- 1 root root 655K 3月  22 15:04 shike
#解压
unzip
例子1： # 解压之前先把原文件删掉，以免冲突
[root@localhost ~]# unzip 1.zip 
[root@localhost ~]# ls -lh
总用量 16M
-rw-r--r-- 1 root root 267K 3月  22 15:25 1.zip
-rw-r--r-- 1 root root 655K 3月  22 14:55 services
-rw-r--r-- 1 root root 655K 3月  22 15:04 shike
```

### rar

```shell
#解压rar包
#需要安装软件
yum install epel-release -y
yum install unar -y
#再进行解压
unar -o 解压路径 被解压文件路径
例如：
 unar -o /opt 456.rar
[root@localhost ~]# ls
1.zip  2.tar.gz  3.tar.gz kaku.rar kaku.tar services shike
[root@localhost ~]# mkdir xx
[root@localhost ~]# unar -o ./xx kaku.rar 
kaku.rar: RAR 5
kaku.txt (49 B)... OK.
Successfully extracted to "./xx/kaku.txt".
[root@localhost ~]# ls xx/
kaku.txt
```

## 软件安装

### 编译安装

我们有时候安装软件，下载下来的是软件源代码，不能直接运行，需要编译之后才能运行，源代码-->编译-->二进制机器码，才能运行。比如windows的某些软件是从源代码编译打包之后才生成exe程序，平常我们接触不到，大家安装的软件都是基本别人编译好的。而linux下编译之后会生成二进制的可执行文件，不是exe程序昂，和windows不同，这种文件没有后缀名。其实linux系统下就没有文件后缀名这个概念，好多后缀名都是我们人工自己加上去的，为了让自己知道文件是干嘛的，主要是给我们自己看的，区分作用。

```shell
我们用一个网站服务软件来玩一玩试试：
1.下载源码包
cd /opt/
rm -fr *
curl -o nginx.tar.gz http://nginx.org/download/nginx-1.20.1.tar.gz
2.编译安装
tar xf nginx.tar.gz 
cd nginx-1.20.1/
   [root@localhost nginx-1.20.1]# ls
   auto CHANGES CHANGES.ru conf configure contrib html LICENSE man 
README src
# 1.配置编译参数
# 这个软件给我们提供了很多功能，我们在编译的过程中可以自己选择哪些功能要，哪些功能不要，所有功能
都要就是完整版，好多功能都不要就成了精简版，比如qq精简版，不知道大家听没听过。
./configure --prefix=/usr/local/nginx --without-pcre --without￾http_rewrite_module --without-http_gzip_module
 #我这里禁掉了一些功能，以为这些功能都需要好多依赖包，大家还不知道依赖包是怎么回事儿，所以我
就暂时先删除了。--without就是去掉的意思。--prefix=/usr/local/nginx是指定软件的安装目录，目
录不存在的话会自动创建。./是用相对路径来执行这个configure文件，用绝对路径也可以执行这个文件。这
个指令执行之后，会自动检查各种依赖环境是否满足软件运行的要求，检查通过之后会生成一个叫做
Makefile的文件。
 [root@localhost nginx-1.20.1]# ls 
   auto     CHANGES.ru configure html     Makefile objs   src
   CHANGES conf       contrib   LICENSE man       README
 #多了两个文件Makefile和objs，刚才的指令主要是为了生成Makefile
# 2.编译
make  #make会找当前目录中的Makefile文件来进行编译，这个编译过程一般是比较长的。到底多长时间
呢？1、看CPU性能 2、软件功能复杂度
 [root@localhost nginx-1.20.1]# ls  
   auto     CHANGES.ru configure html     Makefile objs   src
   CHANGES conf       contrib   LICENSE man       README
 # 编译之后看上去目录结构和之前一样，但是objs目录里面其实多了好多东西。
 [root@localhost nginx-1.20.1]# ls objs/
   autoconf.err nginx   ngx_auto_config.h   ngx_modules.c src
   Makefile     nginx.8 ngx_auto_headers.h ngx_modules.o
 # 其中nginx文件就是我们的二进制可执行的命令文件。它是可执行的程序了，比如我们查看一下它的版
本
 [root@localhost nginx-1.20.1]# ./objs/nginx -v
 nginx version: nginx/1.20.1
 # 到这里只是编译完了，还需要安装，其实安装就是将这个程序的某些文件放到对应的目录中去。其实我
们在上面的编译参数中已经指定好了--prefix=/usr/local/nginx，要安装到/usr/local/nginx目录中
去。
# 3.安装
make install
    # 查看安装目录，这就是它这个软件安装的所有文件
   [root@localhost nginx-1.20.1]# ls /usr/local/nginx/
   conf html logs sbin
 # 这样看目录结构看着不太清晰，我们可以安装一下tree这个工具，来进行目录查看
 [root@localhost nginx-1.20.1]# yum install tree -y
 # 安装完tree之后，我们来看一下目录，看着就清晰多了，树状结构显示。
 [root@localhost nginx-1.20.1]# tree /usr/local/nginx/
   /usr/local/nginx/
   ├── conf  # 该软件的配置文件所在目录
   │   ├── fastcgi.conf
   │   ├── fastcgi.conf.default
   │   ├── fastcgi_params
   │   ├── fastcgi_params.default
   │   ├── koi-utf
   │   ├── koi-win
   │   ├── mime.types
   │   ├── mime.types.default
   │   ├── nginx.conf
   │   ├── nginx.conf.default
   │   ├── scgi_params
   │   ├── scgi_params.default
   │   ├── uwsgi_params
   │   ├── uwsgi_params.default
   │   └── win-utf
   ├── html  # 网站源代码存放目录，这个nginx其实主要是用来部署网站的，网站的代码可以放到这个
目录中
   │   ├── 50x.html
   │   └── index.html
   ├── logs  # 这个软件自带日志记录功能，记录的日志存放在这个目录中
   └── sbin
       └── nginx  # 这个是软件的关键性的启动程序，类似于我们windows安装的qq目录中的QQ.exe
    4 directories, 18 files
3.运行
指令：/usr/local/nginx/sbin/nginx，没有配置环境变量，所以要用完整路径来运行
[root@localhost nginx-1.20.1]# /usr/local/nginx/sbin/nginx
[root@localhost nginx-1.20.1]#   #看上去没什么效果，但是已经运行了
# 可以通过浏览器访问这个nginx了，访问之前要关闭一下防火墙。
# 关闭防火墙
systemctl stop firewalld
# 取消防火墙的开机自启
systemctl disable firewalld
# 使用浏览器访问http://<虚拟机的ip地址>
http://192.168.61.132/ 就可以看到网站了。
二、rpm安装
关于nginx这个软件如何使用，我们后面课程中会详细的讲解，这里先简单感受一下编译安装过程即可。
# 打包：就是将我们编译好的程序打包起来，给其他人用的时候，其他人就不用编译了，因为你已经编译好
了，我们普通用户使用的软件就是别人编译打包之后的软件。
/usr/local/nginx 这个目录就是我们编译好之后的整个软件的所有运行文件目录，我们打包它即可
# 打包压缩
[root@localhost nginx-1.20.1]# cd /usr/local/
[root@localhost local]# ls
bin etc games include lib lib64 libexec nginx sbin share src
[root@localhost local]# tar -zcf /tmp/nginx_kaku.tar.gz nginx 
[root@localhost local]# ls
bin etc games include lib lib64 libexec nginx sbin share src
[root@localhost local]# ls /tmp/
ks-script-ed2ODG
nginx_kaku.tar.gz
# 推送给另外一台主机
[root@localhost tmp]# scp nginx_kaku.tar.gz root@192.168.61.135:/tmp
# 另外一台主机的操作：解压到/usr/local目录下，然后运行
root@localhost tmp]# ls
nginx_kaku.tar.gz
[root@localhost tmp]# mv nginx_kaku.tar.gz /usr/local/
[root@localhost tmp]# cd /usr/local/
[root@localhost local]# ls
bin etc games include lib lib64 libexec nginx_kaku.tar.gz sbin share 
src
[root@localhost local]# tar -zxf nginx_kaku.tar.gz 
[root@localhost local]# ls
bin etc games include lib lib64 libexec nginx nginx_kaku.tar.gz sbin 
share src
[root@localhost local]# /usr/local/nginx/sbin/nginx
[root@localhost local]# systemctl stop firewalld
```

### rpm安装

```shell
# 刚才我们提到过，编译还是比较繁琐的，为了方便使用者，一般都会编译之后发给使用者，用起来不需要编译，就方便多了。只要有人编译一次，将编译后的程序贡献出来，大家就可以用了。所以这些做系统的厂商也发现这样挺好，所以这些厂商干脆将自己的软件也打包一下，redhat、debian等都做了自己软件的打包工作，将自己的软件打包好之后，供用户下载使用。下载软件需要用到对应系统的包管理工具。
# redhat系打出来的包叫做：rpm包。用yum安装的程序包其实都是rmp包。rpm的包我们也可以不使用yum而手动安装。
# debian系打出来的包叫做：deb包。
#rpm全称：redhat package manager包管理器
# 手动安装rpm包示例：不需要编译安装、也不用yum安装。
# 安装wget
yum install wget -y
# 使用wget下载rpm包
wget https://mirrors.tuna.tsinghua.edu.cn/centos/7/os/x86_64/Packages/tree-1.6.010.el7.x86_64.rpm

# 如果没有wget，可以先用curl下载：
curl -o wget.rpm 
https://mirrors.tuna.tsinghua.edu.cn/centos/7/os/x86_64/Packages/wget-1.14-18.el7_6.1.x86_64.rpm
# 安装rpm包 #rpm -i是安装，vh是显示安装进度条的意思。
rpm -ivh tree-1.6.0-10.el7.x86_64.rpm 
# 卸载
rpm -e tree
# 升级
rpm -Uvh xxx.rpm
# 查看已安装的软件
rpm -qa|grep httpd

```

rpm安装软件个小问题，比如：安装vim，会提示安装失败，需要各种依赖包，需要先去安装依赖包，用rpm安装软件不好解决依赖包的问题，所以出来了下面的yum安装方式，自动下载安装需要的依赖包。以后都用yum来安装。

### yum安装

```shell
#自动解决rpm依赖
#yum安装扩展yum仓库
yum install epel-release -y
#yum安装nginx
yum install nginx -y
#yum移除nginx
yum remove nginx -y
#查看仓库rpm的数量
yum repolist
#在软件包名称、描述、摘要等元数据中搜索关键字，返回匹配的软件包列表。
yum search pstree
#查看该命令所属的安装包
yum provides pstree
```

```shell
编译安装：优点： 自由定制 痛点：难度高，步骤繁琐
rpm安装：优点：安装简单   痛点：需要自己解决依赖，不支持定制
yum安装：优点：自动解决依赖，默认安装最新版 痛点：不支持定制
```

## 查看计算机硬件信息

```shell
#查看cpu
lscpu
#查看内存命令
free -h
#查看硬盘命令
df -h  #h表示人类可读
[root@localhost ~]# df -h
文件系统       容量 已用 可用 已用% 挂载点
devtmpfs       980M     0 980M    0% /dev
tmpfs           991M     0 991M    0% /dev/shm
tmpfs           991M  9.5M 981M    1% /run
tmpfs           991M     0 991M    0% /sys/fs/cgroup
/dev/sda1       100G  2.2G   98G    3% /
tmpfs           199M     0 199M    0% /run/user/0
# 含有tmp的表示是内存给硬盘的空间，默认会给1半内存空间，把内存当作硬盘使用，这个我们不用管。
# 如果磁盘空间未满但无法创建新文件，可能是 inode 耗尽。可以使用df -i 查看各文件系统的 inode 使用情况：
[root@localhost ~]# df -ih
文件系统       Inode 已用(I) 可用(I) 已用(I)% 挂载点
devtmpfs        245K     400    245K       1% /dev
tmpfs           248K       1    248K       1% /dev/shm
tmpfs           248K     715    247K       1% /run
tmpfs           248K      16    248K       1% /sys/fs/cgroup
/dev/sda1        50M     59K     50M       1% /
tmpfs           248K       1    248K       1% /run/user/0
tmpfs           248K       1    248K       1% /run/user/1000

#查看计算机的cpu，内存，进程等信息(和windows的任务管理器很像)
top
    top - 08:34:27 up 20 min,  1 user, load average: 0.00, 0.01, 0.05
   Tasks:  89 total,   2 running,  87 sleeping,   0 stopped,   0 zombie
   %Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 
st
   KiB Mem :  2027872 total,  1779000 free,   135668 used,   113204 buff/cache
   KiB Swap:        0 total,        0 free,        0 used.  1755332 avail Mem 
 # 下面是进程信息，值得看的是每个进程占用的%CPU %MEM，CPU使用率和内存使用率
     PID USER     PR NI   VIRT   RES   SHR S %CPU %MEM     TIME+ COMMAND   
           
     1 root      20   0  128556   7132   4144 S  0.0  0.4   0:01.27 systemd     
        
     2 root      20   0       0      0      0 S  0.0  0.0   0:00.00 kthreadd     
       
     4 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 kworker/0:0H
# 08:34:27 up 20 min：表示08:34:27是系统当前时间，开机了20分钟，如果看到3:20，表示开了3小时20分钟，看到10 days表示10天了，linux很稳定耐用，开机好多年都稳定运行着，不会卡顿。
# 1 user ：表示当前只有一个用户在使用
# load average: 0.00, 0.01, 0.05：平均负荷，指的是CPU的负载高不高，CPU负载高，那么平均负荷就比较大，如果这几个值很大的时候，服务器会变得很卡。如果发现服务器卡了，就是异常情况，就可以看看这个数据。这三个值表示：1分钟、5分钟、15分钟的负载情况，load average数据是每隔5秒钟检查一次活跃的进程数，然后按特定算法计算出的数值。如果这个数除以逻辑CPU的数量，结果高于5的时候就表明系统在超负荷运转了。
# Tasks: 89 total， 2 running, 87 sleeping, 0 stopped,   0 zombie：表示进程数量，总共89个，2个正在运行，87个在睡眠状态，当我们的CPU是1核的时候，是在所有进程之间来回切换执行，所以只有一个或者切换速度很快的时候显示2个。 0 stopped表示停止的进程，但是这里一般都是0，因为进程结束之后会自动从内存中释放。0 zombie表示僵尸进程数量，僵尸进程是杀不死的，就是由于各种原因，系统无法自动释放的进程，僵尸进程也消耗系统资源，一般kill掉它的父进程可以杀掉僵尸进程，或者kill -9来杀掉。但是kill -9要慎用！！！它也容易产生僵尸进程，kill会将进程运行中的信息保存下来，进程不会出问题，kill -9不会保存，强制结束进程的运行，容易出现僵尸进程。
# 按数字1，可以查看cpu数量
# %Cpu(s): 0.0 us, 0.0 sy, 0.0 ni,100.0 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st，关于CPU我们其他参数不用看，就看这个100.0 id，id是idle的简写，表示100%空闲，因为我们现在CPU使用率很低，所以显示了100%空闲。我们只关注这个参数即可，看一下CPU忙不忙就行。
# KiB Mem : 2027872 total, 1779000 free,   135668 used,   113204 buff/cache，是内存(英文：memroy)的描述信息，total表示总内存量，free表示可用剩余量，userd表示已经使用的量，buff/cache表示用作缓存，是和磁盘进行读写时的缓存区域，这个参数不用管。
# KiB Swap:       0 total,       0 free,       0 used. 1755332 avail Mem ：Swap表示虚拟内存，这是硬盘分配给内存的一部分空间，为了当内存不足时，临时将硬盘当作内存使用。这个数值是可以自行调整的。一般自动就分配好了，所以我们不用管，实在是内存不够用的时候再加大这个虚拟内存。我现在看的是虚拟机上的虚拟内存，虚拟机不设置虚拟内存,所以显示为0。
```

## date和crontab(定时任务）

定期执行任务（执行命令），和windows的计划任务是一样的。

```shell
例子1：
#查看时间
[root@192 tmp]#  date 
2025年 08月 11日 星期一 17:33:51 CST
[root@192 tmp]# date +%F
2025-08-11
[root@192 tmp]# date +%T
17:34:05
[root@192 tmp]# date +%F\ %T
2025-08-11 17:34:20
例子2：
#修改时间和日期
[root@localhost ~]# date -s '20200723 14:40:00'
2020年 07月 23日 星期四 14:40:00 CST
# 修改时间
[root@localhost ~]# date -s '14:40:00'
#同步时间，如果时间和当前时间不一致，可以做一下时间同步，来让时间准确起来
systemctl restart chronyd # 一次执行完是有延迟的，等待一会才看到准确时间，前提是我们有网

#定时任务的格式
* * * * *   cmd
分 时 日 月 周   命令
分：0-59
时：0-23
日：0-31
月：1-12
周：1-7
#每5分钟执行一次
*/5 * * * *
#每1小时的01分执行一次
01 */1 * * *
#每半个小时执行一次，下面的意思是每小时的00分和30分各执行一次
00,30 */1 * * *
#每天晚上8:00执行一次
00 20 * * *
#每个月1号晚上8:00执行
00 20 1 * *
#每年1月1号晚上8:00执行
00 20 1 1 *
#每周1、周三、周五晚上8:00执行一次
00 20 * * 1,3,5
# 几个符号的意思：
# * 每分钟
# */5 每5分钟
# 05 第5分钟
# 每秒钟执行的任务，需要单独写脚本，繁琐一些。
#查看定时任务，遇到特殊符号%,需要添加转义符号\;
[root@localhost ~]# crontab -l
* * * * *  echo `date +\%T` >>/tmp/time.txt
#编辑定时任务
[root@localhost ~]# crontab -e
示例：
 * * * * * date >> /tmp/time.txt  # 每分钟执行一次
[root@localhost ~]# crontab -l
* * * * * date >> /tmp/time.txt
我们可以通过cat来查看任务是否执行了，但是比较麻烦，每次手动输入cat，所以我们可以用如下指令
tail -f /tmp/time.txt  #监测文件尾部内容的变化.
[root@localhost ~]# tail -f /tmp/time.txt
2023年 03月 24日 星期五 10:58:01 CST
2023年 03月 24日 星期五 10:59:01 CST
2023年 03月 24日 星期五 11:00:01 CST
2023年 03月 24日 星期五 11:01:01 CST
# 是这个进程再帮我们执行定时任务：
[root@localhost ~]# ps -ef|grep cron
root        581      1  0 18:05 ?        00:00:00 /usr/sbin/crond -n
# 我们还可以自行重启这个进程
root@localhost ~]# systemctl restart crond
[root@localhost ~]# ps -ef|grep cron # 可以看到进程启动时间变化了
root       2611      1 25 21:27 ?        00:00:00 /usr/sbin/crond -n
#改为每小时的03分执行
[root@localhost ~]# crontab -e
[root@localhost ~]# crontab -l
03 * * * * date >> /tmp/time.txt
#修改一下系统时间
[root@localhost ~]# date -s '12:02:50'
2023年 03月 24日 星期五 12:02:50 CST
[root@localhost ~]# tail -f /tmp/time.txt
...
2023年 03月 24日 星期五 11:13:01 CST
2023年 03月 24日 星期五 11:14:01 CST
2023年 03月 24日 星期五 12:03:03 CST  # 12点03分执行的
# crontab -e里面每一行都可以写一个定时任务，也就是可以写多个定时任务。
# 比如，再加一个热内：每天晚上9:20自动关机
# 20 21 * * * shutdown -h now
[root@localhost ~]# date -s '21:19:50'
2023年 03月 24日 星期五 21:19:50 CST
[root@localhost ~]# crontab -l
03 * * * * date >> /tmp/time.txt
20 21 * * * shutdown -h now
[root@localhost ~]# date
2023年 03月 24日 星期五 21:21:03 CST
您在 /var/spool/mail/root 中有邮件
# 错误的原因可能是需要我们写shutdown的绝对路径
[root@localhost ~]# which shutdown # which也是查找，可以查找指令的绝对路径
/usr/sbin/shutdown
# 如果指令不行，就写指令的绝对路径，如果定时任务的格式，或者内容有问题，系统都会发邮件提示：
```

##  系统优化

```shell
1.优化ssh，以防连接过慢
vi /etc/ssh/sshd_config  # 改配置文件之前，最好先做好备份，cp /etc/ssh/sshd_config 
/etc/ssh/sshd_config.bak
79行：GSSAPIAuthentication no
115行：UseDNS no  # 别忘了删除前面的注释符号#
systemctl restart sshd

2.优化selinux
#修改配置文件，永久关闭
vi /etc/selinux/config
#第7行修改为
SELINUX=disabled
需要重启生效
#立即生效，临时的 #有时候有些服务器不让重启，就可以先这样临时用一下
setenforce 0

3.关闭firewalld
systemctl stop firewalld
systemctl disable firewalld
4.安装常用软件
yum install lrzsz vim tree wget net-tools screen bash-completion tcpdump -y
# net-tools：网络相关工具，比如ifconfig、ifconfig ens33(只看某个网卡的ip)，rpm -qa是查看安装了哪些rpm包，具体这个软件有哪些命令，可以通过rpm -ql net-tools来查看。
# screen：屏幕工具。
 # 我们以后可能要远程连接某个服务器，比如服务器在国外，那么我们通过本地xshell等远程连接到目标服务器，那么中间有要经过很多个网络设备的传输，很容易断掉连接，如果我们正在执行某个程序，突然断开连接了，那么我们执行的程序也会自动中断，如果我们不想让程序中断，就可以用到screen命令了。
   [root@localhost ~]# screen # 会单独再给我们开启一个终端
   [root@localhost ~]# sleep 100
    # 然后模拟一下，断开连接，在重新连接回来，还可以通过screen恢复到之前的窗口状态，发现程序还在继续执行着。
    
   [root@localhost ~]# screen -ls
   There is a screen on:
        16389.pts-1.localhost (Detached)
    1 Socket in /var/run/screen/S-root.
   [root@localhost ~]# screen -r 16389 # 恢复窗口
    # 所以当网络不稳定的时候最好用screen来操作。
# bash-completion：这个软件很神奇，叫做超级自动补全。这个包安装完之后，要重新登录一下才行。
# 这个工具是tab键的加强版，输入-然后再使用tab的时候可以提示我们有哪些参数了，也就是提示信息更全
了。
[root@localhost ~]# find /etc/ -size 10k -
-amin                   -ignore_readdir_race    -path
-anewer                 -ilname                 -perm
-atime                  -iname                  -print
# 再比如我们想下载某个软件，我记得好像是psm，然后一个tab键就自动补全包名了
[root@localhost ~]# yum install ps
psacct.x86_64       psmisc.x86_64       psutils-perl.noarch psutils.x86_64
 
[root@localhost ~]# rpm -qa|wc -l # 可以查看一下已经安装的软件包

# tcpdump： 
 # 这是个抓包指令，可以抓取网络传输的数据包。用户可以参考下面几个网址：
 # https://www.bbsmax.com/A/WpdKENY1JV/
 # https://www.codenong.com/cs105816177/
 # https://blog.csdn.net/yangshengwei230612/article/details/110878714
```

### tcpdump(抓取网络数据包)

```shell
[root@localhost ~]# tcpdump
# 默认情况下，直接启动tcpdump将监视第一个网络接口(非lo口)上所有流通的数据包，这样抓取的结果会
非常多，而且默认不会显示出来。
[root@localhost ~]# ifconfig # 先查看网卡名称，因为tcpdump抓包的时候和wireshark一样要
指定网卡
ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500
...
# 指定网卡抓取数据包，会将流经这个网卡的数据包全部抓取下来，这样也是太多了，尤其是我们如果是在
xshell上执行这个指令的话，就会看到更多的数据包，刷屏的感觉，是因为xshell是远程连接执行指令，结
果要返回给xshell，都是要经过网卡的。
[root@localhost ~]# tcpdump -i ens33 # 指定网卡名称
# 所以我们用xshell连接来抓包的时候，最好指定端口，比如不抓22端口的，我们抓一下80端口的。
[root@localhost ~]# tcpdump -i ens33 port 80
# 访问：http://192.168.61.139/ 就看到抓取的数据包了
# 将抓取到的数据包保存到pcap\cap文件中，cap是captured的简写，捕获的意思。
[root@localhost ~]# tcpdump -i ens33 port 80 -w jaden.pcap # 屏幕上不显示，也不暂定，
我们ctrl+c停止，然后看到目录下就有文件了
[root@localhost ~]# ls
anaconda-ks.cfg jaden.pcap
# 把jaden.pcap放到我们的物理机，通过wireshark打开来进行查看分析
# -nn参数
# 不加-nn，抓包显示为：20:38:16.924940 IP 192.168.61.1.62552 > 
localhost.localdomain.http: Flags... # 主机名和协议
# 加了-nn，抓包显示为：21:49:01.908068 IP 192.168.61.1.49721 > 192.168.61.139.80: 
Flags # 主机ip地址和端口号
[root@localhost ~]# tcpdump -i ens33 port 80 -nn
# [root@localhost ~]# tcpdump -i ens33 port 80 -nn -c 20 #抓取到20个包之后自动停止
# [root@localhost ~]# tcpdump -i ens33 port 80 -nn -c 20 -S #-S将seq\ack等随机值显
示完整
# 指定协议：
# [root@localhost ~]# tcpdump -i ens33 tcp port 80 -nn -c 20
-i 指定网卡的名称
-nn 不把端口解析成应用层协议
-c 指定抓包的数量
-S 不把随机序列和确认序列解析成绝对值
-w 指定数据包保存的位置
```



## 服务管理

```shell
安装服务
yum install httpd  # 网站服务程序，类似于nginx，它叫做apache
# systemctl 是centos7上专门管理服务的命令
查看所有服务列表
systemctl list-unit-files
启动服务
systemctl  start httpd  #start启动 或者 systemctl start httpd.service
# ps -ef|grep httpd，可以看到服务进程，表示启动了。
停止服务
systemctl  stop   httpd  #stop停止
重启服务
systemctl  restart   httpd #restart重启，就是关闭再开启
查看服务状态
systemctl status   httpd  #查看服务状态
把服务设置为开机启动
systemctl enable httpd.service
取消服务的开机自启
systemctl disable httpd.service
```

## 环境变量

```shell
  env命令可以查看系统内置的环境变量：和windows的环境变量类似。系统变量就是让一些在调用的时候比较麻烦或者说寻找的时候路径比较长的功能变得简单化。系统内部处理时，会根据变量的值做出不同的反应。
   [root@localhost ~]# env
        XDG_SESSION_ID=1
        HOSTNAME=localhost.localdomain # 变量作用：比如HOSTNAME这个变量，它的值比较长，系统内部程序会经常用到这个值，那么用一个变量存放，以后想用这个值，就用这个变量即可，简单很多，而且只要修改了这个值，其他使用这个变量的地方，值都会跟着变化，方便修改。
        TERM=xterm
        SHELL=/bin/bash
 HISTSIZE=1000  # 这就是为什么历史命令只记录1000的原因。
 SSH_CLIENT=192.168.61.1 50670 22
        SSH_TTY=/dev/pts/0
        USER=root  # 当前登录用户，其他用户登录的时候，这个变量对应的值就变为了其他用户名
       ...
 LANG=zh_CN.UTF-8  # language的简写，装系统的时候，你安装的英文，这里就是en_US，中文就是zh_CN
 ...
 # 查看某个变量的值 $符号+变量名称：
 [root@localhost ~]# echo $LANG
 zh_CN.UTF-8
 # 我们改一下语言变量，来看看效果，比如之前命令的参数介绍都是中文的,export用来声明环境变量、修改环境变量等，如下：
 [root@localhost ~]# usermod --help
       用法：usermod [选项] 登录
       选项：
          -c, --comment 注释           GECOS 字段的新值
          -d, --home HOME_DIR           用户的新主目录
 ...
 [root@localhost ~]# export LANG=en_US.UTF-8
 [root@localhost ~]# usermod --help # 全部变英文了
       Usage: usermod [options] LOGIN
       Options:
          -c, --comment COMMENT         new value of the GECOS field
          -d, --home HOME_DIR           new home directory for the user account
 ...
 # 也就是说，改动环境变量，会对系统有影响，因为系统中使用这个变量的功能都会随着变量的值而做不同的处理。
```

## Linux常用特殊符号

```shell
1. ""双引号，换行，解析变量
比如：echo，本来只能输出单行文本内容，加上双引号支持换行输入和输出
   [root@localhost ~]# echo hello
   hello
守夜人Jaden-吴老板
   [root@localhost ~]# echo "hello
   > kaku
   > "
   hello
   kaku
   [root@localhost ~]# echo "hello
   kaku
    " > kaku.txt # 还可以输出到某个文件中
   [root@localhost ~]# cat kaku.txt
   hello
   kaku
   有时候比vi用起来方便。
    # ""能够解析变量，如下
   [root@localhost ~]# echo "$LANG"
 en_US.UTF-8
2.''单引号，换行，不解析变量
 # 单引号不能解析变量，其他功能和双引号类似，如下
 [root@localhost ~]# echo '$LANG'
 $LANG
3.\和/ #这些我们都说过
   \ 转义符，反斜杠
   / 路径分隔符
4.! 历史命令调用，在find命令中是取反的意思。
 [root@localhost ~]# history
 [root@localhost ~]# !47 # 历史指令序号
5.* 通配符，我们将find的之后用到过，可以匹配任意字符
 [root@localhost ~]# ls *.txt # 查看所有.txt结尾的文件
 kaku.txt
6.$ 调用变量
   例子1：
   [root@localhost ~]# export LANG='en_US.UTF-8'
   [root@localhost ~]# echo $LANG 
   en_US.UTF-8
   [root@localhost ~]# stat 111.txt 
     File: ‘111.txt’
     Size: 0         Blocks: 0         IO Block: 4096   regular empty file
   Device: fd00h/64768d Inode: 33575641   Links: 1
   Access: (0777/-rwxrwxrwx) Uid: (    0/   root)   Gid: (    0/   root)
   Access: 2021-09-12 04:40:28.399177386 +0800
   Modify: 2021-09-12 04:40:28.399177386 +0800
   Change: 2021-09-12 04:40:28.400260737 +0800
     Birth: -
   [root@localhost ~]# export LANG='zh_CN.UTF-8'
   [root@localhost ~]# stat 111.txt 
     文件："111.txt"
     大小：0         块：0         IO 块：4096   普通空文件
   设备：fd00h/64768d Inode：33575641   硬链接：1
```

## Linux运行级别

运行级别 0 关机
运行级别 1 单用户 ，这个类似于windows安全模式，可以用于找回密码等操作。
运行级别 2 不带网络的多用户 ，这种是不能联网的。
运行级别 3 完整的多用户模式 multi-user.target ， 我们平常使用的模式
运行级别 4 保留
运行级别 5 桌面模式 graphical.target ， 桌面版系统就是这个模式，如果不想开机进入图形化界面，就需要修改运行级别，可以试一下
运行级别 6 重启
centos6是通过数字来设置，centos7都不是用数字了，而是用下面的方式，不过数字设置依然有效：

```shell
#切换运行级别
init 
# 执行init 6，就会重启，执行init 0就会关机
#查看运行级别
runlevel
#设置运行级别，设置之后一重启就改变了
systemctl set-default graphical.target   #设置默认运行级别为图形，注意没有安装图形化界面工具的话是不能切换为桌面版的
systemctl set-default multi-user.target  #设置默认运行级别为命令行
```

centos7单用户运行级别修改root密码：https://blog.csdn.net/yu_bingbing/article/details/123555427

## 权限掩码

### 掩码

```shell
# 查看掩码值
[root@localhost ~]# umask
0022
```

这个值就决定着我们创建文件的初始权限，比如我们创建个目录和文件，如下:

```shell
[root@localhost ~]# mkdir kaku
[root@localhost ~]# touch wulaoban.txt
[root@localhost ~]# ll -h
总用量 4.0K
-rw-------. 1 root root 1.3K 3月  15 20:14 anaconda-ks.cfg
drwxr-xr-x  2 root root    6 3月  27 09:29 kaku
-rw-r--r--  1 root root    0 3月  27 09:29 wulaoban.txt
# 可以看到，目录的初始权限为755，文件的初始权限为644。这些权限都是通过umask掩码计算得来的。
# 文件权限计算：0666-0022 = 0644
# 目录权限计算：0777-0022 = 0755
```

我们还可以修改掩码值来控制初始文件和文件夹的权限：

```shell
#修改文件vim /etc/profile，找到umask来修改
root     默认权限掩码 022  
普通用户 默认权限掩码 002
```

### inode和lock

inode ：存储除文件以外的属性，比如文件路径，inode全称index node，索引节点的意思。索引主要是用于方便我们进行文件查找的。我们也叫它为目录文件。

block： 存储文件的内容。

```shell
[kaku@localhost ~]$ df -h #查看硬盘空间
文件系统       容量 已用 可用 已用% 挂载点
devtmpfs       980M     0 980M    0% /dev
tmpfs           991M     0 991M    0% /dev/shm
tmpfs           991M  9.6M 981M    1% /run
tmpfs           991M     0 991M    0% /sys/fs/cgroup
/dev/sda1       100G  2.0G   98G    2% /
tmpfs           199M     0 199M    0% /run/user/0
tmpfs           199M     0 199M    0% /run/user/1000
[kaku@localhost ~]$ df -ih  # 查看inode空间
文件系统       Inode 已用(I) 可用(I) 已用(I)% 挂载点
devtmpfs       245K     369   245K       1% /dev
tmpfs           248K       1   248K       1% /dev/shm
tmpfs           248K     707   247K       1% /run
tmpfs           248K      16   248K       1% /sys/fs/cgroup
/dev/sda1       50M     60K     50M       1% /
tmpfs           248K       1   248K       1% /run/user/0
tmpfs           248K       1   248K       1% /run/user/1000
```

可以看到我们的虚拟机，硬盘100G，inode空间为50M，所以其实硬盘会划分两个空间，一个是存数据的空间，一个是存文件索引的空间。每个文件会用多个block块来存储，这个block就类似于windows上我们说的簇，文件数据的最小存放空间单元，每个文件都会有一条目录索引记录到inode空间中，方便以后我们找寻找个文件。

> 我们在linux上创建文件的时候，可能会看到一个报错信息： No space left on device ，意思是没有可用空间了。说明要么是硬盘确实存满了，要么是inode空间存满了，如果是inode空间存满了，那么就去删除那些临时文件或者一些无用的空文件、小文件等等来清理inode空间。

## suid(特殊权限)

suid，就是某个可执行文件有super超级管理员权限，这个文件普通用户也能用，含有suid的文件，可以让普通用户拥有该文件属主的执行权限，主要针对的是命令文件。比如：

```shell
例子1：
passwd 是用来修改密码的一个命令文件
[root@localhost ~]# passwd kaku  
#看一下passwd文件的权限
[root@localhost ~]# ll /usr/bin/passwd 
-rwsr-xr-x. 1 root root 27856 4月   1 2020 /usr/bin/passwd
# 可以看到ugo权限组合中的u权限rws，这个s其实就是x权限，但是s就是用来标记这个文件是一个具有suid权限的特殊执行文件。由于权限位只有9位，所以特殊权限的执行权限用s代替了x。
# 有执行权限的时候是小写的s，去掉用户的执行权限之后，这个地方是大写的S。如下
[root@localhost ~]# chmod u-x /usr/bin/passwd 
[root@localhost ~]# ll /usr/bin/passwd 
-rwSr-xr-x. 1 root root 27856 4月   1 2020 /usr/bin/passwd
# 再将执行权限加回来，看效果，又变回了小s
[root@localhost ~]# ll /usr/bin/passwd 
-rwsr-xr-x. 1 root root 27856 4月   1 2020 /usr/bin/passwd
# 那么，为什么会给这个文件一个叫做suid的权限呢？这个文件是用来修改密码的执行文件，普通用户是不是也可以修改自己的密码啊，对吧，但是修改密码修改的是/etc/shadow文件内容，看一下/etc/shadow文件
权限：
[root@localhost ~]# ll /etc/shadow
---------- 1 root root 768 3月  27 10:45 /etc/shadow
# /etc/shadow文件权限是000，普通用户根本就没有修改这个文件的权限。因为如果普通用户能修改这个文件，那么root用户的密码就能被普通用户修改了，这就很不安全，对吧。但是每次改密码都找root用户，也是很麻烦的，所以普通用户也有自己改密码的需求，这怎么办。比如我们登录一下普通用户，修改一下密码试试
[kaku@localhost ~]$ passwd
更改用户 kaku 的密码 。
为 kaku 更改 STRESS 密码。
（当前）UNIX 密码：   # 普通用户修改密码，必须要输入原来的密码，root用户不需要
新的 密码：  # 而且密码复杂度要高，比如我设置的是123@qq.com，才行
无效的密码： 密码少于 8 个字符
[kaku@localhost ~]$ passwd
更改用户 kaku 的密码 。
为 kaku 更改 STRESS 密码。
（当前）UNIX 密码：
新的 密码：
重新输入新的 密码：
passwd：所有的身份验证令牌已经成功更新。
# 普通用户修改密码其实比较麻烦，要输入原密码、还要将密码复杂度加高。
# 普通用户也要用passwd修改密码，有这种需求，所以给系统给passwd执行文件了一个特殊权限，就是s。
[root@localhost ~]# ll /usr/bin/passwd 
-rwsr-xr-x. 1 root root 27856 4月   1 2020 /usr/bin/passwd
# 那么普通用户使用这个文件的时候，可以拥有这个文件属主的执行权限，也就是root的x权限。所以我们看到普通用户可以使用passwd来修改自己的密码，这就是suid权限的意思，但是只能修改当前自己的用户密码，而且是用的root身份来执行的，如下，用普通用户修改一下root用户的密码，看看效果
[kaku@localhost ~]$ passwd root
passwd：只有根用户才能指定用户名。 # 只有root用户才能指定用户名来修改某个用户的密码，普通用户不能指定用户名，只能修改自己的。
# 如果将passwd文件的s权限去掉了，那么普通用户就没有修改密码的能力了，如下
[root@localhost ~]# chmod u-s /usr/bin/passwd
[root@localhost ~]# ll /usr/bin/passwd 
-rwxr-xr-x. 1 root root 27856 4月   1 2020 /usr/bin/passwd
# 切换到普通给用户修改密码看效果：
[kaku@localhost ~]$ passwd
更改用户 kaku 的密码 。
为 kaku 更改 STRESS 密码。
（当前）UNIX 密码：
新的 密码：  # abc.123.xx
重新输入新的 密码：
passwd: 鉴定令牌操作错误
# 发现密码修改不了了。因为passwd没有了suid权限。
# 我们把suid权限再给加回去就可以了。
[root@localhost ~]# chmod u+s /usr/bin/passwd 
[root@localhost ~]# ll /usr/bin/passwd 
-rwsr-xr-x. 1 root root 27856 4月   1 2020 /usr/bin/passwd
例子2：
netstat -ltp
# root用户身份运行，结果如下
[root@localhost ~]# netstat -ltp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       
PID/Program name    
tcp        0      0 0.0.0.0:ssh             0.0.0.0:*               LISTEN     
1185/sshd           
tcp        0      0 localhost:smtp          0.0.0.0:*               LISTEN     
1330/master         
tcp6       0      0 [::]:ssh               [::]:*                 LISTEN     
1185/sshd           
tcp6       0      0 localhost:smtp         [::]:*                 LISTEN     
1330/master
#普通用户运行，结果如下
[kaku@localhost ~]$ netstat -ltp #p参数普通用户不能使用
(No info could be read for "-p": geteuid()=1000 but you should be root.) # 看到了一个报错提示，并且PID数据没显示
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       
PID/Program name    
tcp        0      0 0.0.0.0:ssh             0.0.0.0:*               LISTEN     
-                   
tcp        0      0 localhost:smtp          0.0.0.0:*               LISTEN     
-                   
tcp6       0      0 [::]:ssh               [::]:*                 LISTEN     
-                   
tcp6       0      0 localhost:smtp         [::]:*                 LISTEN     
-
# 给netstat执行文件加上suid权限
[root@localhost ~]# chmod u+s /usr/bin/nestat 
[root@localhost ~]# ll /usr/bin/netstat 
-rwsr-xr-x. 1 root root 155008 8月   9 2019 /usr/bin/netstat
#普通用户再运行，就不报错了，而且看到了PID数据
[kaku@localhost ~]$ netstat -ltp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       
PID/Program name    
tcp        0      0 0.0.0.0:ssh             0.0.0.0:*               LISTEN     
1185/sshd           
tcp        0      0 localhost:smtp          0.0.0.0:*               LISTEN     
1330/master         
tcp6       0      0 [::]:ssh               [::]:*                 LISTEN     
1185/sshd           
tcp6       0      0 localhost:smtp         [::]:*                 LISTEN     
1330/master
#加上suid权限，就表示普通用户使用这个执行文件的时候，会用root的身份来运行。
#这是suid的作用，但是好多黑客利用它来进行恶意的权限提升
```

## Linux普通用户提权

### sudo提权

就是我们进行sudo授权时给的授权太高，或者给授权时控制的不合理，就会被普通用户利用来提权。

```shell
示例1：
vim  # 命令模式执行: !/
 # 通过vim修改/etc/sudoers，授权ALL
 # 再通过vim进入一个文件
 # :输入指令，是可以直接输入系统指令的，前面加一个!即可，比如创建一个文件，!touch 3.txt
 # 查看3.txt信息如下
 [kaku@localhost ~]$ ll
   总用量 0
    -rw-r--r-- 1 root root  0 3月  27 17:05 3.txt  # 以root用户身份创建的文件
 # 如果在vim文件时，执行!/bin/bash，就进入到了root的命令终端，可以为所欲为。
 # 这就是sudo提权，但是sudo提权需要借助到可以执行系统指令的交互式的功能，比如vim。
示例2：
 find # sudo find . -exec bash \; # 直接进入root的命令终端，这个指令退出root终端可能要退好几次才行，看find找到了几个文件，找到了3个文件，就输入三次exit才能退出。
示例3：
 awk  # sudo awk 'BEGIN {system("/bin/bash")}' kaku.txt # 直接进入到root命令终端，exit直接退出。
 
# 还有好多指令可以提权，比如cp命令也可以提权，将其他电脑上的/etc/shadow文件拷贝到这个系统中，密码就改掉了，再su切换到root即可等等，还有什么mv、vi、sed修改文件、chmod改重要文件权限等等这里就不多提了。大家可以试试，普通用户使用sudo来修改shadow文件的root用户的密码。
```

### 脏牛提权

dcow全称dirty cow，脏牛，原理：Linux内核的内存子系统在处理写入时复制（copy-on-write, COW，

组合起来是牛的意思）时产生了竞争条件。恶意用户可利用此漏洞，来获取高权限，对只读内存映射进

行写访问，所以大家都管这个提权方式叫做脏牛提权。原理这一块大家不需要掌握，会监测是否存在这

个漏洞即可。

```shell
仓库地址：https://github.com/gbonacini/CVE-2016-5195，先下载下来。
# github上对它有介绍，比如哪些版本的系统有这样的漏洞。要某个系统版本和gcc版本同时满足的时候才会有这个漏洞。
```

