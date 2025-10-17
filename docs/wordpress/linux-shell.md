---
layout: default
title: LinuxShell脚本攻略
parent: wordpress
---

## 目录

- [《linux就该这么学》](#linux就该这么学)
- [LinuxShell脚本攻略](#LinuxShell脚本攻略)
  - [ch01](#ch01)
    - [1.15 持续运行命令直至执行成功](#115-持续运行命令直至执行成功)
  - [ch02](#ch02)
    - [2.3 录制并回放终端会话](#23-录制并回放终端会话)
    - [2.4 查找并列出文件](#24-查找并列出文件)
      - [1. 根据文件名或正则表达式进行搜索](#1-根据文件名或正则表达式进行搜索)
      - [2. 否定参数 find也可以用!排除匹配到的模式](#2-否定参数-find也可以用排除匹配到的模式)
      - [3. 基于目录深度的搜索](#3-基于目录深度的搜索)
      - [4. 根据文件类型搜索](#4-根据文件类型搜索)
      - [5. 根据文件的时间戳进行搜索](#5-根据文件的时间戳进行搜索)
      - [6. 基于文件大小的搜索](#6-基于文件大小的搜索)
      - [7. 基于文件权限和所有权的匹配](#7-基于文件权限和所有权的匹配)
      - [8. 利用find执行相应操作](#8-利用find执行相应操作)
      - [让find跳过特定的目录](#让find跳过特定的目录)
    - [2.5 玩转 xargs](#25-玩转-xargs)
    - [2.6 用 tr 进行转换](#26-用-tr-进行转换)
    - [2.12 根据扩展名切分文件名](#212-根据扩展名切分文件名)
    - [2.13 多个文件的重命名与移动](#213-多个文件的重命名与移动)
    - [2.16 利用并行进程加速命令执行](#216-利用并行进程加速命令执行)
  - [ch05-一团乱麻？没这回事](#ch05-一团乱麻没这回事)
  - [5.2 Web 页面下载](#52-Web-页面下载)
    - [5.3 以纯文本形式下载页面](#53-以纯文本形式下载页面)
    - [5.7 图片爬取器及下载工具](#57-图片爬取器及下载工具)
    - [5.14 从 Internet 下载视频](#514-从-Internet-下载视频)
  - [ch08](#ch08)
    - [8.11 使用 SSH 实现端口转发](#811-使用-SSH-实现端口转发)
  - [ch09](#ch09)
    - [9.6 使用 watch 监视命令输出](#96-使用-watch-监视命令输出)
    - [9.7 记录文件及目录访问情况](#97-记录文件及目录访问情况)
    - [9.8 使用 syslog 记录日志](#98-使用-syslog-记录日志)
  - [ch10](#ch10)
    - [10.8 使用 cron 进行调度](#108-使用-cron-进行调度)
  - [ch13](#ch13)
    - [13.4 在 Linux 中使用虚拟机](#134-在-Linux-中使用虚拟机)

# 《linux就该这么学》读书笔记

|System V init 命令 （RHEL 6 系统） |systemctl 命令（RHEL 7 系统） |作用|
|:--:|:--:|:--:|
|service foo start |systemctl start foo.service |启动服务|
|service foo restart |systemctl restart foo.service |重启服务|
|service foo stop |systemctl stop foo.service |停止服务|
|service foo reload |systemctl reload foo.service |重新加载配置文件（不终止服务）| |service foo status |systemctl status foo.service |查看服务状态|
|chkconfig foo on |systemctl enable foo.service |开机自动启动|
|chkconfig foo off |systemctl disable foo.service |开机不自动启动|
|chkconfig foo |systemctl is-enabled foo.service | 查看特定服务是否为开机自动启动|
|chkconfig --list |systemctl list-unit-files --type=service |查看各个级别下服务的启动与禁用情况|

# 《LinuxShell脚本攻略》读书笔记

## ch01

### 1.15 持续运行命令直至执行成功

repeat() { while :; do \$@ && return; sleep 30; done } 

## ch02

### 2.3 录制并回放终端会话

script命令能够录制你的击键以及击键时机，并将输入和输出结果保存在对应的文件中。scriptreplay命令可以回放会话。

甚至可以调用其他解释器并录制发送给该解释器的击键。但你无法记录vi、emacs或其他将字符映射到屏幕特定位置的应用程序。

```bash
$ script -t 2> timing.log -a output.session
```


可以指定一个文件名作为script命令的参数。该文件将保存击键及命令结果。如果指定了-t选项，script命令会把时序数据发送到stdout。可以将这些数据重定向到其他文件中（timing.log），这样该文件中就记录了每次击键的时机以及输出信息。上面的例子中使用2>将
stderr重定向到了文件timing.log。
利用文件timing.log和output.session，可以按照下面的方法回放命令执行过程：

```bash
$ scriptreplay timing.log output.session
```


### 2.4 查找并列出文件

find命令的工作方式如下：沿着文件层次结构向下遍历，匹配符合条件的文件，执行相应
的操作。默认的操作是打印出文件和目录，这也可以使用-print选项来指定。

要列出给定目录下所有的文件和子目录，可以采用下面的语法：

```bash
$ find base_path
```


print选项使用\n（换行符）分隔输出的每个文件或目录名。而-print0选项则使用空字符
'\0'来分隔。-print0的主要用法是将包含换行符或空白字符的文件名传给xargs命令。随后会
详细讨论xargs命令：

```bash
$> echo "test" > "file name" 
$> find . -type f -print | xargs ls -l 
ls: cannot access ./file: No such file or directory 
ls: cannot access name: No such file or directory 
$> find . -type f -print0 | xargs -0 ls -l 
-rw-rw-rw-. 1 user group 5 Aug 24 15:00 ./file name
```


上面的例子演示了如何使用find列出文件层次中所有的文件和目录。find命令能够基于通

配符或正则表达式、目录树深度、文件日期、文件类型等条件查找文件。

#### 1. 根据文件名或正则表达式进行搜索

-name选项指定了待查找文件名的模式。这个模式可以是通配符，也可以是正则表达式。在

下面的例子中，' \*.txt'能够匹配所有名字以.txt结尾的文件或目录。

\$ find /home/slynux -name ' \*.txt' -print
find命令有一个选项-iname（忽略字母大小写）

find命令支持逻辑操作符。-a和-and选项可以执行逻辑与（AND）操作，-o和-or选项可 以执行逻辑或（OR）操作。 

\$ ls new\.txt some.jpg text.pdf stuff.png 

\$ find . ( -name '*.txt' -o -name '*.pdf' ) -print ./text.pdf ./new\.txt 

上面的命令会打印出所有的.txt和.pdf文件，因为这个find命令能够匹配所有这两类文件。\ （以及\）用于将 -name '*.txt' -o -name '*.pdf'视为一个整体。

-path选项可以限制所匹配文件的路径及名称。例如，\$ find /home/users -path '*/slynux/*' -name ' \*.txt' –print能够匹配文件/home/users/slynux/readme.txt，但无法匹 配/home/users/slynux.txt。 -regex选项和-path类似，只不过前者是基于正则表达式来匹配文件路径的。

-iregex选项可以让正则表达式在匹配时忽略大小写

#### 2. 否定参数 find也可以用!排除匹配到的模式

\$ find . ! -name " \*.txt" -print 上面的find命令能够匹配所有不以.txt结尾的文件

#### 3. 基于目录深度的搜索

find命令在查找时会遍历完所有的子目录。默认情况下，find命令不会跟随符号链接。-L
选项可以强制其改变这种行为。但如果碰上了指向自身的链接，find命令就会陷入死循环中。
-maxdepth和–mindepth选项可以限制find命令遍历的目录深度。这可以避免find命令没
完没了地查找。
/proc文件系统中包含了系统与当前执行任务的信息。特定任务的目录层次相当深，其中还
有一些绕回到自身（loop back on themselves）的符号链接。系统中运行的每个进程在proc中都有
对应的子目录，其名称就是该进程的进程ID。这个目录下有一个叫作cwd的链接，指向进程的当
前工作目录。
下面的例子展示了如何列出运行在含有文件bundlemaker.def的目录下的所有任务：
\$ find -L /proc -maxdepth 1 -name 'bundlemaker.def' 2>/dev/null 

 2>/dev/null将有关循环链接的错误信息发送到空设备中 
-mindepth选项类似于-maxdepth，不过它设置的是find开始进行查找的最小目录深度。
这个选项可以用来查找并打印那些距离起始路径至少有一定深度的文件。

-maxdepth和-mindepth应该在find命令中及早出现。如果作为靠后的选
项，有可能会影响到find的效率，因为它不得不进行一些不必要的检查。

#### 4. 根据文件类型搜索

将文件和目录分别列出可不是件容易事。不过有了find就好办了。例如，只列出普通文件：
\$ find . -type f -print 

表 2-1 
文件类型 类型参数
普通文件 f 
符号链接 l 
目录 d 
字符设备 c 
块设备 b 
套接字 s 
FIFO p 

#### 5. 根据文件的时间戳进行搜索

Unix/Linux文件系统中的每一个文件都有3种时间戳，如下所示。
 访问时间（-atime）：用户最近一次访问文件的时间。
 修改时间（-mtime）：文件内容最后一次被修改的时间。
 变化时间（-ctime）：文件元数据（例如权限或所有权）最后一次改变的时间。
Unix默认并不保存文件的创建时间。但有一些文件系统（ufs2、ext4、zfs、
btrfs、jfs）会选择这么做。可以使用stat命令访问文件创建时间。
鉴于有些应用程序通过先创建一个新文件，然后再删除原始文件的方法来修
改文件，文件创建时间未必准确。
-atime、-mtime和-ctime可作为find的时间选项。它们可以用整数值来
指定天数。这些数字前面可以加上-或+。-表示小于，+表示大于。
考虑下面的例子。
打印出7分钟之前访问的所有文件：
\$ find . -type f -amin +7 -print 

找出比file.txt修改时间更近的所有文件：
\$ find . -type f -newer file.txt -print 

find命令的时间戳处理选项有助于编写系统备份和维护脚本。

#### 6. 基于文件大小的搜索

大于2KB的文件 

\$ find . -type f -size +2k

#### 7. 基于文件权限和所有权的匹配

列出具有特定权限的文件：

\$ find . -type f -perm 644 -print 

打印出权限为644的文件

#### 8. 利用find执行相应操作

find命令能够对其所查找到的文件执行相应的操作。无论是删除文件或是执行任意的Linux
命令都没有问题。
(1) 删除匹配的文件

\$ find . -type f -name " \*.swp" -delete

(2) 执行命令

利用-exec选项，find命令可以结合其他命令使用。

find命令使用一对花括号{}代表文件名。在下面的例子中，对于每一个匹配的文件，find

命令会将{}替换成相应的文件名并更改该文件的所有权。如果find命令找到了root所拥有的两个

文件，那么它会将其所有者改为slynux：

find . -type f -user root -exec chown slynux {} \\; 

注意该命令结尾的\\;。必须对分号进行转义，否则shell会将其视为find命

令的结束，而非chown命令的结束。

为每个匹配到的文件调用命令可是个不小的开销。如果指定的命令接受多个参数（如

chown），你可以换用加号（+）作为命令的结尾。这样find会生成一份包含所有搜索结果的列

表，然后将其作为指定命令的参数，一次性执行。

另一个例子是将给定目录中的所有C程序文件拼接起来写入单个文件all\_c\_files.txt。各种实现

方法如下：

\$ find . -type f -name ' \*.c' -exec cat {} ;>all\_c\_files.txt

\$ find . -type f -name ' \*.c' -exec cat {} > all\_c\_files.txt ;

\$ fine . -type f -name ' \*.c' -exec cat {} >all\_c\_files.txt +

我们使用 > 操作符将来自find的数据重定向到all\_c\_files.txt文件，没有使用>>（追加）的原

因是find命令的全部输出就只有一个数据流（stdin），而只有当多个数据流被追加到单个文件

中时才有必要使用>>。

下列命令可以将10天前的 .txt文件复制到OLD目录中：

\$ find . -type f -mtime +10 -name " \*.txt" -exec cp {} OLD ;

find命令还可以采用类似的方法与其他命令结合使用。

我们无法在-exec选项中直接使用多个命令。该选项只能够接受单个命令，

不过我们可以耍一个小花招。把多个命令写到一个 shell脚本中（例如

[command.sh](http://command.sh "command.sh")），然后在-exec中使用这个脚本：

-exec ./commands.sh {} \\; 

-exec可以同printf搭配使用来生成输出信息。例如：

\$ find . -type f -name " \*.txt" -exec printf "Text file: %s\n" {} ;

Config file: /etc/openvpn/easy-rsa/openssl-1.0.0.cnf 

Config file: /etc/my.cnf 

#### 让find跳过特定的目录

在搜索时排除某些文件或目录的技巧叫作修剪。下面的例子演示了如何使用-prune选项排
除某些符合条件的文件：
\$ find devel/source\_path -name '.git' -prune -o -type f -print 

### 2.5 玩转 xargs

xargs命令从stdin处读取一系列参数，然后使用这些参数来执行指定命令。它能将单行或
多行输入文本转换成其他格式

zargs命令重新格式化stdin接收到的数据，再将其作为参数提供给指定命令。xargs默认
会执行echo命令。和find命令的-exec选项相比，两者在很多方面都相似。
 将多行输入转换成单行输出。
xargs默认的echo命令可以用来将多行输入转换成单行输出：
\$ cat example.txt # 样例文件
1 2 3 4 5 6 
7 8 9 10 
11 12 
\$ cat example.txt | xargs 
1 2 3 4 5 6 7 8 9 10 11 12 
 将单行输入转换成多行输出。
xargs的-n选项可以限制每次调用命令时用到的参数个数。下面的命令将输入分割成多
行，每行N个元素：
\$ cat example.txt | xargs -n 3 
1 2 3 
4 5 6 
7 8 9 
10 11 12 

如果文件或目录名中包含空格（甚至是换行）的话，使用空白字符来分割输入就会出现问题。

我们可以定义一个用来分隔参数的分隔符。-d选项可以为输入数据指定自定义的分隔符：
$echo "splitXsplit2Xsplit3Xsplit4" | xargs -d X 
Split1 split2 split3 split4 
在上面的代码中，stdin中是一个包含了多个X字符的字符串。我们可以用–d选项将X定义为
输入分隔符。
结合-n选项，可以将输入分割成多行，每行包含两个单词：$ echo "splitXsplitXsplitXsplit" | xargs -d X -n 2
split split
split split
xargs命令可以同find命令很好地结合在一起。find的输出可以通过管道传给xargs，由后
者执行-exec选项所无法处理的复杂操作。如果文件系统的有些文件名中包含空格，find命令的
-print0选项可以使用0（NULL）来分隔查找到的元素，然后再用xargs对应的-0选项进行解
析。下面的例子在Samba挂载的文件系统中搜索.docx文件，这些文件名中通常会包含大写字母和
空格。其中使用了grep找出内容中不包含image的文件：
\$ find /smbMount -iname ' \*.docx' -print0 | xargs -0 grep -L image

### 2.6 用 tr 进行转换

tr只能通过stdin（标准输入）接收输入（无法通过命令行参数接收）。其调用格式如下：
tr \[options] set1 set2 
来自stdin的输入字符会按照位置从set1映射到set2（set1中的第一个字符映射到set2
中的第一个字符，以此类推），然后将输出写入stdout（标准输出）。set1和set2是字符类或字符组。如果两个字符组的长度不相等，那么set2会不断复制其最后一个字符，直到长度与set1
相同。如果set2的长度大于set1，那么在set2中超出set1长度的那部分字符则全部被忽略。

定义集合也很简单，不
需要书写一长串连续的字符序列，只需要使用“起始字符终止字符”这种格式就行了。这种写
法也可以和其他字符或字符类结合使用。如果“起始字符终止字符”不是有效的连续字符序列，
那么它就会被视为含有3个元素的集合（起始字符、和终止字符）。你也可以使用像'\t'、'\n'
这种特殊字符或其他ASCII字符。

在ROT13算法中，字符会被移动13
个位置，因此文本加密和解密都使用同一个函数：
\$ echo "tr came, tr saw, tr conquered." | tr 'a-zA-Z' 'n-za-mN-ZA-M' 

1. 用tr删除字符

tr有一个选项-d，可以通过指定需要被删除的字符集合，将出现在stdin中的特定字符清

除掉：

\$ cat file.txt | tr -d '\[set1]' 

\#只使用set1，不使用set2 

例如：

\$ echo "Hello 123 world 456" | tr -d '0-9' 

Hello world 

将stdin中的数字删除并打印删除后的结果

1. 字符组补集

我们可以利用选项-c来使用set1的补集。下面的命令中，set2是可选的：

tr -c \[set1] \[set2] 

如果只给出了set1，那么tr会删除所有不在set1中的字符。如果也给出了set2，tr会将不

在set1中的字符转换成set2中的字符。如果使用了-c选项，set1和set2必须都给出。如果-c

与-d选项同时出现，你只能使用set1，其他所有的字符都会被删除。

下面的例子会从输入文本中删除不在补集中的所有字符：

\$ echo hello 1 char 2 next 4 | tr -d -c '0-9 \n' 

124 

接下来的例子会将不在set1中的字符替换成空格：

\$ echo hello 1 char 2 next 4 | tr -c '0-9' ' ' 

1 2 4 

1. 用tr压缩字符

tr命令能够完成很多文本处理任务。例如，它可以删除字符串中重复出现的字符。基本实现

形式如下：

tr -s '\[需要被压缩的一组字符]'

用tr以一种巧妙的方式
将文件中的数字列表进行相加：
\$ cat sum.txt 
1 
2 
3 
4 
5 
\$ cat sum.txt | echo $\[ \$(tr '\n' '+' ) 0 ] 
15 
这招是如何起效的？
在命令中，tr命令将'\n'替换成了'+'，我们因此得到了字符串1+2+3+..5+，但是在字符
串的尾部多了一个操作符+。为了抵消这个多出来的操作符，我们再追加一个0。
$\[ operation ]执行算术运算，因此就形成了以下命令：
echo $\[ 1+2+3+4+5+0 ] 

### 2.12 根据扩展名切分文件名

借助%操作符可以从name.extension这种格式中提取name部分（文件名）。下面的例子从 sample.jpg中提取了sample： file\_jpg="sample.jpg" name=${file_jpg%. *} echo File name is:  $name\*

输出结果： Extension is: jpg 2.12.2 工作原理 在第一个例子中，我们使用了%操作符从形如name.extension的格式中提取出了文件名。 \${VAR%. \*} 的含义如下。  从$VAR中删除位于%右侧的通配符（在上例中是.*）所匹配的字符串。通配符从右向左进 行匹配。  给VAR赋值，即VAR=sample.jpg。通配符从右向左匹配到的内容是.jpg，因此从$VAR中 删除匹配结果，得到输出sample。 %属于非贪婪（non-greedy）操作。它从右向左找出匹配通配符的最短结果。还有另一个操作 符%%，它与%相似，但行为模式却是贪婪的，这意味着它会匹配符合通配符的最长结果。

\#操作符可以从文件名中提取扩展名。这个操作符与%类似，不过求值方向是从左向右。\${VAR# \*.}

从\$VARIABLE中删除位于#右侧的通配符（即在上例中使用的 \*.）从左向右所匹配到的字 符串。 和%%类似，#也有一个对应的贪婪操作符##

### 2.13 多个文件的重命名与移动

rename命令利用Perl正则表达式修改文件名。组合find、rename和mv命令，我们能做到的
事其实很多。

### 2.16 利用并行进程加速命令执行

parallel命令从stdin中读取文件列表，使用类似于find命令的-exec选项来处理这些文
件。符号{}代表被处理的文件，符号{.}代表无后缀的文件名。
下面的命令使用了Imagemagick的convert程序来为目录中的所有图像创建新的缩放版本：
ls \*jpg | parallel convert {} -geometry 50x50 {.}Small.jpg

## ch05-一团乱麻？没这回事

## 5.2 Web 页面下载

由于不稳定的互联网连接，下载有可能被迫中断。选项-t可以指定在放弃下载之前尝试多
少次：
\$ wget -t 5 URL 
将-t选项的值设为0会强制wget不断地进行重试

选项--limit-rate可以限定下载任务能够占有的最大 带宽，从而保证其他应用程序能够公平地访问Internet: \$ wget --limit-rate 20k [http://example.com/file.iso](http://example.com/file.iso "http://example.com/file.iso")

如果wget在下载完成之前被中断，可以利用选项-c从断点开始继续下载：
\$ wget -c URL

复制整个网站（镜像）

wget像爬虫一样以递归的方式遍历网页上所有的URL链接，并逐个下载。要实现这种操作，

可以使用选项--mirror：

\$ wget --mirror --convert-links [exampledomain.com](http://exampledomain.com "exampledomain.com") 

或者

\$ wget -r -N -l -k DEPTH URL 

选项-l指定页面层级（深度）。这意味着wget只会向下遍历指定层数的页面。该选项要与-r

（recursive，递归选项）一同使用。另外，-N表示使用文件的时间戳。URL表示欲下载的网站起始地

址。-k或--convert-links指示wget将页面的链接地址转换为本地地址。

对网站进行镜像时，请三思而行。除非获得许可，否则你只应出于个人使用

的目的才可以这么做，而且不要频繁地做镜像。

1. 访问需要认证的HTTP或FTP页面

一些网站需要HTTP或FTP认证，可以用--user和--password提供认证信息：

\$ wget --user username --password pass URL 

### 5.3 以纯文本形式下载页面

Web页面其实就是包含HTML标签、JavaScript和CSS的文本文件。HTML标签定义了页面内
容，如果要解析页面来查找特定的内容，这时bash就能派上用场了。可以用浏览器查看HTML文
件格式是否正确，也可以用之前讲过的工具对其进行处理。
解析文本文件要比解析HTML数据来得容易，因为不用再去剥离HTML标签。Lynx是一款基
于命令行的Web浏览器，能够以纯文本形式下载Web网页

选项-dump能够以纯ASCII编码的形式下载Web页面。下面的命令可以将下载到的页面保存 到文件中： \$ lynx URL -dump > webpage\_as\_text.txt 这个命令会将页面中所有的超链接（[）作为文本文件的页脚，单独放置在标 题为References的区域。这样我们就可以使用正则表达式专门解析链接了。](link "）作为文本文件的页脚，单独放置在标 题为References的区域。这样我们就可以使用正则表达式专门解析链接了。")

### 5.7 图片爬取器及下载工具

```bash
if [ $# -ne 3 ]; 
then 
 echo "Usage: $0 URL -d DIRECTORY" 
 exit -1 
fi 

while [ $# -gt 0 ] 
do 
 case $1 in 
 -d) shift; directory=$1; shift ;; 
 *) url=$1; shift;; 
 esac 
done 
mkdir -p $directory; 
baseurl=$(echo $url | egrep -o "https?://[a-z.\-]+") 
echo Downloading $url 
curl -s $url | egrep -o "<img[^>]*src=[^>]*>" | \ 
 sed 's/<img[^>]*src=\"\([^"]*\).*/\1/g' | \ 
 sed "s,^/,$baseurl/," > /tmp/$$.list 
cd $directory; 
while read filename; 
do 
 echo Downloading $filename 
 curl -s -O "$filename" --silent 
done < /tmp/$$.list

```


使用方法：
\$ url=<https://commons.wikimedia.org/wiki/Main_Page> 
\$ ./img\_downloader.sh \$url -d images 

5.7.2 工作原理
图片下载器脚本首先解析HTML页面，除去\<img>之外的所有标签，然后从\<img>标签中解
析出src="URL"并将图片下载到指定的目录中。这个脚本接受一个Web页面的URL和用于存放图
片的目录作为命令行参数。 
\[ \$# -ne 3 ]用于检查脚本参数数量是否为3个。如果不是，脚本会退出运行并显示使用
说明。如果参数没有问题，就解析URL和目标目录：

while循环会一直处理完所有的参数。shift用来向左移动参数，这样\$2的值就会被赋给 \$1，
\$3的值被赋给 \$2，往后以此类推。因此通过 \$1就可以求值所有的参数。

case语句检查第一个参数（$1）。如果匹配-d，那么下一个参数一定是目录，接着就移动参 数并保存目录名。否则的话，就是URL。 采用这种方法来解析命令行参数的好处在于可以将-d置于命令行中的任意位置： $ ./img\_downloader.sh -d DIR URL 或者 \$ ./img\_downloader.sh URL -d DIR egrep -o "!]\(\[^)] *>"只打印带有属性值的标签。\[^>]* 用来匹配除>之外 的所有字符，也就是<img src="image.jpg">。

 sed 's/!\[ /tmp/\$\$.list 最后的while循环用来逐行迭代图片的URL列表并使用curl下载图像文件。curl的 --silent选项可避免在屏幕上出现下载进度信息。

### 5.14 从 Internet 下载视频

有一个叫作youtube-dl的视频下载工具。多数发行版中并没有包含这个工具，软件仓库里 的版本也未必是最新的，因此最好是去官方网站下载（[http://yt-dl.org](http://yt-dl.org "http://yt-dl.org")）。

将视频的URL复制/粘贴到 youtube-dl的命令行中： youtube-dl [https://www.youtube.com/watch?v=AJrsl3fHQ74](https://www.youtube.com/watch?v=AJrsl3fHQ74 "https://www.youtube.com/watch?v=AJrsl3fHQ74")

youtube-dl通过向服务器发出GET请求（就像浏览器一样）来实现视频下载。它会伪装成浏览器，使得YouTube或其他视频提供商以为这是一台流媒体设备，从而下载到视频。
选项-list-formats（-F）会列出支持的视频格式，选项-format（-f）可以指定下载哪
种格式的视频。如果你的Internet连接带宽不足，而你又想下载高分辨率视频的时候，这个选项就
用得上了。

## ch08

### 8.11 使用 SSH 实现端口转发

## ch09

### 9.6 使用 watch 监视命令输出

watch命令会按照指定的间隔时间来执行命令并显示其输出。你可以使用终端会话和第10章
中描述的screen命令创建一个自定义的控制面板（dashboard），利用watch监视系统的运行情况。

以30秒为间隔，着重标记出新的网络连接
\$ watch -n 30 -d 'ss | grep ESTAB' 

### 9.7 记录文件及目录访问情况

inotifywait命令会监视文件或目录并报告何时发生了某种事件。Linux发行版默认并没有
包含该命令，你得用软件包管理器自行安装inotify-tools

记录指定路径中的创建、移动以及删除事件。选项-m表示持续监视变化，而
不是在事件发生之后退出。选项-r允许采用递归形式监视目录（忽略符号链接）。选项-e指定需要监视的事件列表。选项-q用于减少冗余信息，只打印出所需要的信息。命令输出可以被重定向
到日志文件

### 9.8 使用 syslog 记录日志

与守护进程和系统进程相关的日志文件位于/var/log目录中。在Linux系统中，由守护进程
sylogd使用syslog标准协议处理日志。每一个标准应用程序都可以利用syslogd记录日志。在这
则攻略中，我们将讨论如何在脚本中用syslogd进行日志记录。

## ch10

### 10.8 使用 cron 进行调度

GNU/Linux系统包含了多种任务调度的工具，其中cron的应用最为广泛。它允许任务能够按
照固定的时间间隔在系统后台自动运行。cron使用了一个表（crontab），表中保存了需要执行的
一系列脚本或命令以及执行时间。

所有的GNU/Linux发布版默认都包含了cron调度工具。它会扫描cron表，确定其中是否有
需要执行的命令。每个用户都有自己的cron表，这其实就是一个纯文本文件。crontab命令用
于处理cron表。

当cron执行命令的时候是以该表项创建者的身份执行的，但
它不会去执行该用户的.bashrc文件。如果命令需要使用环境变量，必须在crontab中定义。

执行cron作业所使用的权限同创建crontab的用户的权限相同。如果你需要执行要求更高
权限的命令，例如关闭计算机，那么就要以root用户身份执行crontab命令。
在cron作业中指定的命令需要使用完整路径。这是因为cron并不会执行用户的.bachrc，所
以执行cron作业时的环境与终端所使用的环境不同，环境变量PATH可能都没有设置。如果命令
运行时需要设置某些环境变量，必须明确地进行设定。

## ch13

### 13.4 在 Linux 中使用虚拟机

在Linux中使用虚拟机共有4种选择。前3种开源方案分别是KVM、XEN和VirtualBox。后一
种商业方案是VMware，它提供了一个客居于（hosted）Linux系统的虚拟化引擎和一个能够运行
虚拟机的可执行程序。
VMware支持虚拟机的历史比其他对手都要久。它支持Unix、Linux、Mac OS X和Windows
作为宿主系统（host），Unix、Linux和Windows作为宾客系统（guest）。就商业应用而言，VMware 
Player和VMware Workstation是两种最佳选择。
KVM和VirtualBox是Linux中最流行的两个虚拟机引擎。KVM的性能要更好，但是要求CPU
支持虚拟化（Intel VT-x）。如今大多数Intel和AMD的CPU都支持该特性。VirtualBox的优势在于
跨平台：Windows和Mac OS X下也可以使用，便于将虚拟机挪到其他平台。VirtualBox不要求VT-x
支持，因此既适合于遗留系统，也适合于现代系统。

