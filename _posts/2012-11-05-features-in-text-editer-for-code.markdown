---
layout: post
title: 编程用的文本编辑器应该具有的功能
date: 2012-11-05 10:12
comments: true
categories: program
---

本文列举写代码用的文本编辑器应该有哪些功能
每行最后的命令就是vi中对应的命令，注意有些是插件的功能，不是vi本身的功能，并且快捷键是我自己用的，可以自定义

## 基本文本操作

* 插入字符，单词，行，段落 a, A, o, O, I, i
* 删除字符，单词，行，段落 x, dw, d$, d)
* 合并行，上移本行，下移本行 J, ddkP, ddp
* 插入，撤销行注释，块注释 cmd+/, gcp
* 书签 m
* 大小写转换 ~
* 查找替换，是否区分大小写，正则支持等 ?, /
* 撤销，重做 u, Ctrl+r
* 编码支持，utf-8，gb2312，gbk等 encoding等
* 全文查找，所选择部分查找，文件夹查找，工程文件中查找
* 全屏
* 多栏 vv, ss
* 拼写检查
* 词典
* 文件切换，上一个，下一个 ,z  ,x  ,lj
* 主题
* FTP、SCP支持


## 代码相关

* 关键词高亮
* 换行符转换
* 添加、移除utf-8 BOM头
* 高亮当前行
* 标尺
* 函数定义，类定义
* 自动完成，参数提示 Ctrl + n
* 代码片段 TAB
* 方法列表，变量列表 ,T
* 方法查找 ,f
* 括号配对，HTML标签配对 %
* 格式化代码 =
* CSS颜色预览
* 代码折叠 zc, zo
* 格式化粘贴
* console
* 宏 q, @
* 多标签支持 cmd+t
* 等宽字体支持
* 格式化文本，缩进 =, <<, >>
* 跨平台，终端支持
* SCM工具支持，git, svn等
* 代码校验，错误提示 quickfix
* build工具支持，make, rake等 !
* 插件支持

## finally
我没有用过Emacs，所以我只推荐vim  
我用的vim配置是[这里](https://github.com/skwp/dotfiles)的，已经配置好了，自带了很多插件，而且针对html，ruby等做了优化，非常好用，建议直接clone一份下来，这样就不用自己折腾了  
如果你觉得这个配置还是不好使，你可以自己折腾一套vim的配置，然后放到github上共享给大家~

### reference
* <http://zh.wikipedia.org/zh/%E6%96%87%E4%BB%B6%E7%BC%96%E8%BE%91%E5%99%A8%E6%AF%94%E8%BE%83>
* <https://github.com/skwp/dotfiles>







