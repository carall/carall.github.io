---
layout: post
---

## 0. RE & wildcard

**sed,grep和awk都是linux下非常强大的文件操作程序，除awk外以行为单位操作。他们都是管道命令，都要频繁使用到正则表达式。**

## 1. sed (stream editor 流编辑器)

**以行为单位对文件进行各种操作**

	sed [-nefri] '[n1[,n2]] [aicdps] [str]'

***

* n : silent  只会显示被改变的行
* e : more than one command 可以做多次操作
* f : 
* r : extended reguler expression 使用扩展的正则表达式
* i : write the file 对文件做更改

***

**[n1[,n2]]** : 选择作操作的行，有两种选择方法：

	1. n1,n2 或者 n ($ 表示末行)
	2. /regular expression/
	
***

* **a/i +str**: 在行首/行尾插入str 
* **c +str**: 用 str 替换改行 
* **s/str_old/str_new/g**: 选择，然后替换，可以使用正则表达式
* **d**: 删除行
* **p**: 打印行

## 2.grep(global regular expression print)

**全局正则表达式打印：以行为单位，按照某些匹配规则，选择某一/几行并把他们输出**

	grep [-acinv] [-An] [-Bn] 'str' file

* a : binary 二进制文件
* c : count 计行数
* i : ignore case 忽略大小写
* n : row number 输出行号
* v : reverse 输出没有被匹配的行
* **str** : RE avaliable 要匹配的字符串，可以使用正则表达式
* [-An]/[-Bn] : 输出匹配行的前/后 n 行

## 3.awk

	awk 'option1{command1}option2{command2}'

**awk支持对文件以字符为单位的操作，可以理解为awk命令就是一个循环，循环周期为每一行。**

#### 3.1 Built-in(内置变量)
* **NF** : 当前循环（行）的字段总数
* **NR** ：当前循环的行号
* **FS** : seperator 字段分割字符，默认为空格
* **$0 $1 $2...** ： 整行数据 第一个字段 第二个字段。。。（注意和shell里面$0 $1的区分）

#### 3.2 BEGIN and END

*可以当做是awk命令中的option选项 (option一般设置为选择条件)：*

	BEGIN { }   END { }

* **BEGIN** : 在awk命令循环开始之前就要进行的操作，一般用来设置FS
* **END** : 在awk命令循环结束之后的操作，一般用来设置输出

#### 3.3 command

* 输出：print(change line) and printf(don't change line)
* 循环：`for while if` 与c语言中的语法一样（是不是因为awk是c语言写的？）
* 变量前不使用$符号，也与c语言一样

#### 3.4 communication with shell
