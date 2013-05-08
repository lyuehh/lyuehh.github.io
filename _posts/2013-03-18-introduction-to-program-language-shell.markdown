---
layout: post
title: 编程语言入门介绍之 - shell
date: 2013-03-18 17:33
comments: true
categories: program
---

## 1 简介
维基百科介绍: <https://en.wikipedia.org/wiki/Shell_script>  
shell是类Unix系统如[Linux][1], [MacOS][2], [FreeBSD][3]中用户与内核进行交互操作的接口,
它接受用户输入的命令, 并把它送入内核执行.  
常见的shell有[bash][4], [ksh][5], [zsh][6]等, 它们的语法大致类似, 有些许区别, 这里就不介绍了..
shell脚本语言是一种解释性语言, 没有像C语言那样的编译阶段,由shell直接解析后执行.  

## 2 语法

### 2.1 赋值

```
foo=3
```

注意不能写成`foo = 3`, 因为shell脚本里的每一行都是要在命令执行的, 所以`foo = 3`在shell看来,
它表示调用一个叫`foo`的程序, 并且传递给它了2个参数`=`和`3`, 系统里并没有一个叫`foo`的程序,
所以肯定会报错.  如果你执意要在`=`两边加上空格的话,可以这样写`(( foo = 3))`.  赋值后使用变量:
```
echo $foo
```
也就是调用变量的时候,要在变量前加上`$`.
可以把赋值和调用写在一行上,中间用`;`分割, 如果一行只有一个语句,可以省略`;`
```
foo=3;echo $foo
```
在字符串中引用变量:
```
bar=3
foo="bar is $bar";echo $foo
```
如果变量名后面会有其他字符,那么可以用`{}`把变量名引起来:
```
bar=3
foo="bar is ${bar}lalala~~~";echo $foo
```
一个变量可以包含多个值:
```
foo=(1 2 3);echo $foo
```
shell中的变量是无类型的, 默认变量均为字符型.

### 2.2 三种引号
看例子就明白了:
```
# 双引号
foo=3
echo "foo is $foo" # -> foo is 3
echo "pwd is `pwd`" # -> pwd is /Users/yourname
echo "foo\tis\t$foo" # -> foo	is	3

# 单引号
foo=3
echo 'foo is $foo' # -> foo is $foo
echo 'pwd is `pwd`' # -> pwd is `pwd`
echo 'foo\tis\t$foo' # -> foo	is	$foo
```
1. 反引号`(就是键盘上1左边那个键)中的内容会被shell当做系统命令执行
2. 双引号会解释变量, 执行反引号里的命令, 也会解释转义字符
3. 单引号不会解释变量,也不会执行反引号内的命令,但是会解释转义字符


### 2.3 运算符
和大多其他编程语言类似:
`#`后面的内容表示注释.

```
+ # $((3+5)) -> 8
- # $((5-3)) -> 2
* # $((3*5)) -> 15
/ # $((5/3)) -> 1
% # $((5%3)) -> 2
```

复合赋值运算符:
```
+=
-=
*=
/=
%=
```

位运算符:
```
<<
>>
&
!
~
^
```

自增自减:
```
++
--
```

### 2.4 测试结构
测试命令用于测试表达式的真假, 如果测试条件为真,返回一个0值;否则,返回一个非0值.
测试命令有2中,使用test命令`test expression`, 其中的`expression`可以为算数运算符,也可以是文件属性等;
另一种是方括号语法`[ expression ]`, 注意`[`之后和`]`之前的空格必不可少,因为`[`本身是一个命令, 后面的
都是这个命令的参数, 而`]`是它的最后一个参数.

#### 2.4.1 整数比较运算符
```
[ n1 -eq n2 ] # 相等比较,如果n1和n2相等,返回0
[ n1 -ge n2 ] # 大于或等于比较
[ n1 -gt n2 ] # 大于比较
[ n1 -le n2 ] # 小于或等于比较
[ n1 -lt n2 ] # 小于比较
[ n1 -ne n2 ] # 不相等比较
```
示例
```
[ 5 -eq 5 ]
echo $? # $?表示最后一条命令的执行结果
```

#### 2.4.2 浮点数比较
shell默认只支持整数之间的计算和比较, 如果需要进行浮点数计算或比较,需要用到`bc`这个命令.
```
# 比较两个浮点数
echo "5.4 > 3.2" | bc # -> 1 # bc结果为1表示结果为真
echo "4.3 * 1.2 " | bc # -> 5.1
```
更多的用法请查看`bc`的帮助手册, `man bc`.

#### 2.4.3 字符串比较

```
[ -n string ] #测试字符串string是否不为空
[ -z tring ]  #测试字符串string是否为空
[ str1 = str2 ] #测试str1是否与str2相同
[ str1 != str2 ] #测试str1是否域str2不相同
```
测试字符串时,建议使用双引号将字符串引起来.

#### 2.4.4 文件操作符
```
[ -d /etc/passwd ] #测试文件是否为目录
[ -e file ] # 测试文件是否存在
[ -f file ] # 测试文件是否为普通文件
[ -s file ] # 测试文件的长度是否不为0
[ -r file ] # 测试文件是否为进程可读文件
[ -w file ] # 测试文件是否为进程可写文件
[ -x file ] # 测试文件是否为进程可执行文件
[ -L file ] # 测试文件是否为符号链接
```

#### 2.4.5 逻辑运算符
逻辑运算符用来测试多个条件是否为真或为假.
```
[ ! expression ] # 如果expression为真, 则测试结果为假
[ expre1 -a expre2 ] # 如果expre1和expr2同时为真, 则判断结果为真
[ expre1 -o expre2 ] # 如果expre1和expr2中有一个为真, 则结果为真
```
示例:
```
[ -e /etc/passwd -a -d /etc ] # -> 0, 结果为真
```

### 2.5 控制结构

#### 2.5.1 条件判断
if语句:
```
if expression
then
  echo 'true'
fi
# then 语句可以和if语句写到一行上, 但是一定要加上分号
if expression; then
  echo 'true'
fi

# else
if expression; then
  echo 'true'
else
  echo 'false'
fi

# 多个else
if expression1; then
  echo 'expr1 true'
elif expression2; then
  echo 'expr2 true'
elif expression3; then
  echo 'expr3 true'
fi
```

#### 2.5.2 switch case
和`if else`语句不同,switch case语句只能比较字符串常量或者正则表达式.
```
case var in
  start)
    echo 'start';
    ;;
  stop)
    echo 'stop';
    ;;
  restart)
    echo 'restart';
    ;;
  *)
    echo 'other';
    ;;
esca
```

#### 2.5.3 循环

for循环:
```
for var in (list)
do
  echo $var
done
```
示例:
```
for var in 1 2 3 4 5
do
  echo $var
done

# 或者和其他命令一起使用
for l in `ls`
do
  echo $l
done
```
类C风格的for循环:
```
for ((i = 1; i <= 5; i++))
do
  echo $i
done
```

while循环:
```
i=1
while [ $i -le 5 ]
do
  echo $i
  i=$(( $i+1 ))
done

# 也可以用另一种语法
i=1
while (( $i <= 5 ))
do
  echo $i
  i=$(( $i+1 ))
done
```

until循环:
until循环和while循环类似, 但是until是在判断条件为假时继续执行, 直到判断条件为真时停止循环.
```
i=1
util (( $i > 5 )) # -> 和while的条件刚好相反
do
  echo $i
  i=$(( $i+1 ))
done

# 也可以用另一种语法

i=1
util [ $i -gt 5 ]
do
  echo $i
  i=$(( $i+1 ))
done
```
### 2.6 重定向 管道
重定向用来向程序输入数据, 或者将一个命令的输出结果保存到一个文件.
```
cat < until.sh # 将until.sh的内容传递给cat命令
# 当然cat命令可以接受文件名作为参数, 你可以直接执行`cat until.sh`

ls > a.txt # 将ls命令的返回结果保存到a.txt这个文件, 如果a.txt不存在,则会创建,如果已经存在,则会覆盖里面的内容
ls -alg >> a.txt #将命令的结果追加到a.txt文件末尾
```
管道和重定向类似, 但是它是将一个命令的输出作为下一个命令的输入.
```
cd / # 切换到根目录
ls | grep var # 使用管道符,在ls命令的返回值里查找var这个字符串
```

### 2.7 函数
定义一个函数:
```
hello()
{
  echo "hello"
}
```
调用函数:
```
hello # -> hello
```
向函数传递参数:
```
hello()
{
  echo "hello $1"
}
hello aaa # -> hello aaa
```
给函数传递参数时, 参数之间用空格分割, $1表示第1个参数, $2表示第二个参数, 依此类推...
$#表示参数的个数

## end
大概就是这些, 其他细节, 还有很多没有提到的, 请参考相关书籍或者手册...

[1]: http://zh.wikipedia.org/wiki/linux
[2]: http://zh.wikipedia.org/wiki/Mac
[3]: http://zh.wikipedia.org/wiki/Freebsd
[4]: http://zh.wikipedia.org/wiki/Bash
[5]: http://zh.wikipedia.org/wiki/Ksh
[6]: http://zh.wikipedia.org/wiki/Zsh
