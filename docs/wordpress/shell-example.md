---
layout: default
title: shell例程
parent: wordpress
---

# shell例程

## 目录

- [随机打乱文件](#随机打乱文件)
- [基本循环](#基本循环)
- [使用函数和参数](#使用函数和参数)
- [包含源文件](#包含源文件)
- [检索返回码和输出](#检索返回码和输出)
- [以上来自《Bash Cookbook》](#以上来自Bash-Cookbook)
- [\[\](http://bj.apsonic-moto.cn/2021/07/07/shell-program-demo/#3-8-%E5%BE%AA%E7%8E%AF "3.8 循环")3.8 循环](#httpbjapsonic-motocn20210707shell-program-demo3-8-E5BEAAE78EAF-38-循环38-循环)
- [\[\](http://bj.apsonic-moto.cn/2021/07/07/shell-program-demo/#5-4-trap%EF%BC%9A%E6%8D%95%E8%8E%B7%E4%B8%AD%E6%96%AD "5.4 trap：捕获中断")5.4 trap：捕获中断](#httpbjapsonic-motocn20210707shell-program-demo5-4-trapEFBC9AE68D95E88EB7E4B8ADE696AD-54-trap捕获中断54-trap捕获中断)
- [\[\](http://bj.apsonic-moto.cn/2021/07/07/shell-program-demo/#ch04-%E8%BF%87%E6%BB%A4%E7%A8%8B%E5%BA%8F "ch04 过滤程序")ch04 过滤程序](#httpbjapsonic-motocn20210707shell-program-democh04-E8BF87E6BBA4E7A88BE5BA8F-ch04-过滤程序ch04-过滤程序)
  - [\[\](http://bj.apsonic-moto.cn/2021/07/07/shell-program-demo/#4-1-grep%E5%AE%B6%E6%97%8F "4.1 grep家族")4.1 grep家族](#httpbjapsonic-motocn20210707shell-program-demo4-1-grepE5AEB6E6978F-41-grep家族41-grep家族)
  - [\[\](http://bj.apsonic-moto.cn/2021/07/07/shell-program-demo/#4-2-%E5%85%B6%E4%BB%96%E8%BF%87%E6%BB%A4%E7%A8%8B%E5%BA%8F "4.2 其他过滤程序")4.2 其他过滤程序](#httpbjapsonic-motocn20210707shell-program-demo4-2-E585B6E4BB96E8BF87E6BBA4E7A88BE5BA8F-42-其他过滤程序42-其他过滤程序)
  - [\[\](http://bj.apsonic-moto.cn/2021/07/07/shell-program-demo/#4-3-%E6%B5%81%E7%BC%96%E8%BE%91%E7%A8%8B%E5%BA%8Fsed "4.3 流编辑程序sed")4.3 流编辑程序sed](#httpbjapsonic-motocn20210707shell-program-demo4-3-E6B581E7BC96E8BE91E7A88BE5BA8Fsed-43-流编辑程序sed43-流编辑程序sed)

### 随机打乱文件

```bash
mkdir `date +%y%m%d`
for i in */*
do
mv "$i" `date +%y%m%d`/$RANDOM.mp3
done
```

### 基本循环
do while循环
```
#!/bin/bash  
CTR=1  
while [ ${CTR} -lt 9 ]  
do  
 echo ${CTR}  
 ((CTR++))  
done
```

### 使用函数和参数
```
#!/bin/bash function print2() {
local lhs="$1"
local rhs="$2"
echo "${lhs} ${rhs}"
}
print2 "a" "b"
```

### 检索返回码和输出

三种方式

1. 使用全局变量保存命令的返回码
2. 使用return
3. 通过echo输出，使用子shell获取

# 以上来自《Bash Cookbook》

---

# 以下来自《Unix编程环境》

## 3.8 循环
```
for i in *; do diff -b old/$i $i; echo; done | pr -h 'title' | lpr &
for i in 3 4 5 6; do ln 2 $i; done
for i in `cat ...`
for i in `pick *`  #交互式选择文件
do
    echo $i
done
```

## 5.4 trap：捕获中断

发出中断信号，后台运行的进程（使用&运行）能得到保护；但如果是挂断信号，则得不到保护。

`trap 命令序列 信号值列表`，命令序列最好用单引号来保护，这样变量仅在trap程序执行时才被赋值

trap调用的命令结束后，程序返回到断点继续执行，除非中断信号终止了它或显式地调用exit

# ch04 过滤程序

## 4.1 grep家族
```
grep -y mary $HOME/lib/phone-book  
ls | grep -v temp
```
选项-v表示对测试结果求反，-y使得模式中的小写字母与文件中的大小写字母都相匹配

grep的正则表达式不能与换行符匹配，表达式被独立地应用于每一行

egrep附加了圆括号、或操作符、加号和问号：
```
(xy)*  
today|tomorrow
egrep -e '^(.?)(.?)(.?)(.?)(.?)(.?)(.?)(.?)(.?).?\9\8\7\6\5\4\3\2\1$' file
#可以查最长为19的回文字符串
```

fgrep不能解释元字符，但却可有效地并行检索成千上万个单词

egrep和fgrep都接受-f选项表示从指定的文件中读取模式

## 4.2 其他过滤程序

sort的选项：-f忽略大小写、-d字典序、-n数值序、-r降序、+m跳过头m个域、-o输出文件、-u删除排序区域中的重复行
`sort +4f +3n -t ':' /etc/passwd`
可使用多个排序码

unique的选项：-d只打印重复的行、-u只打印唯一的行、-c对每行的出现进行计数

comm用于文件比较。它打印三列输出：仅在f1中出现的行、仅在f2中出现的行、在两者出现的行
```
tr A-Z a-z    #将大写字母映射成小写字母  
tr -sc A-Za-z '\012'    #将非字母字符转换为换行
```

dd常被用于处理原始的、未格式化的数据


