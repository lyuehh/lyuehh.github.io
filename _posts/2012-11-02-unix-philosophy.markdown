---
layout: post
title: unix设计哲学
date: 2012-11-02 12:42
comments: true
categories: program
---

Unix哲学是一套由Unix开发者提出的软件开发的准则和哲学。

## 1
[Douglas Mallroy](http://en.wikipedia.org/wiki/Douglas_McIlroy)是Unix系统中管道的发明者，也是Unix文化的缔造者，他曾经说过：

* 让每个程序就做好一件事，如果有新任务，就重新开始，不要往原程序中加入新功能
* 假定每个程序的输出都会成为另一个程序的输入，哪怕那个程序还是未知的，输出中不要有无关的信息干扰，避免使用严格的分栏格式和二进制输入，不要坚持使用交互式输入
* 尽可能早地将设计和编译的软件投入试用，哪怕操作系统也不例外，理想情况下是几个星期内。对拙劣的代码不要犹豫，扔掉重写
* 优先使用工具而不是拙劣的帮助来减轻编程任务的负担。工欲善其事，必先利其器

后来他这样总结：

* 一个程序只做一件事，并做好
* 程序要能协作
* 程序要能处理文本流，这是最通用的接口

## 2
[罗勃·派克](http://zh.wikipedia.org/wiki/%E7%BE%85%E5%8B%83%C2%B7%E6%B4%BE%E5%85%8B)在他的书[Notes on Programming in C](http://www.lysator.liu.se/c/pikestyle.html)中提到了以下格言，虽然这些准则是关于程序设计的，但是作为Unix哲学也毫不为过：

1. 遇到程序的瓶颈时，在没有找到问题之前，不要胡乱修改代码
2. 测试代码，找到瓶颈所在
3. 处理小问题时不需要使用功能全面的算法
4. 复杂的算法更容易产生bug，尽量使用简单的算法和数据结构
5. 数据压倒一切，选择正确的数据结构，就会有正确的算法
6. 没有准则6

第一、二条准则被[高德纳](http://zh.wikipedia.org/wiki/%E9%AB%98%E5%BE%B7%E7%BA%B3)称为：
> 过早的优化是一切罪恶的根源

第三、四条准则被[肯·汤普逊](http://zh.wikipedia.org/wiki/%E8%82%AF%C2%B7%E6%B1%A4%E6%99%AE%E9%80%8A)修改为：
> 疑惑不定之时做事和穷举

## 3
[The UNIX Philosophy](http://en.wikipedia.org/wiki/Unix_philosophy)中提出了以下9条格言：

1. 小即是美
2. 让程序只做好一件事
3. 尽可能早地建立原型
4. 可移植性比效率更重要
5. 数据应保存为文本文件
6. 尽可能地榨取软件的全部价值
7. 使用shell脚本来提高效率和可移植性
8. 避免使用可定制性低下的用户界面
9. 所有程序都是数据的过滤器

### reference

* <http://zh.wikipedia.org/zh/Unix%E5%93%B2%E5%AD%A6>
* <http://www.ruanyifeng.com/blog/2009/06/unix_philosophy.html>














