---
layout: post
title: 使用goacccess分析nginx日志
date: 2012-09-09 16:17
comments: true
categories: program
---

最近要统计一下访问网站的用户的浏览器情况，网上搜了一下，找到了这个[goaccess][1]，还有[这个][2]，看了一下，还算符合要求，就下载然后试用了一下，记录下过程。

## 安装
这个就是`./configure; make; make install`，如果报错了那就是缺少依赖，按照[这里][3]的要求安装依赖，然后应该就差不多了。

## 配置
服务器用的是Nginx，先把访问日志从服务器上拖了过来，本来想在服务器上直接分析的，种种原因还是先放到本地分析一下看看再说。。
日志格式大概是这样的:
```
[27/Jul/2012:00:05:46 +0800],125.34.134.194,-,xxx@xxx.com,GET /xxx HTTP/1.1,692,42.588,0,499,"http://xxx","Mozilla/5.0 (Windows NT 5.1) AppleWebKit/535.18 (KHTML, like Gecko) Chrome/18.0.1010.1 Safari/535.18"
[27/Jul/2012:00:05:46 +0800],125.34.134.194,-,xxx@xxx.com,GET /xxx HTTP/1.1,679,44.484,0,499,"http://xxx","Mozilla/5.0 (Windows NT 5.1) AppleWebKit/535.18 (KHTML, like Gecko) Chrome/18.0.1010.1 Safari/535.18"
[27/Jul/2012:00:05:46 +0800],223.202.24.72,-,xxx@xxx.com,GET /xxx HTTP/1.1,704,0.008,60,200,"http://xxx","Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 5.2; WOW64; Trident/4.0; .NET CLR 2.0.50727; .NET CLR 3.0.04506.648; .NET CLR 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 3.5.30729; .NET4.0C; .NET4.0E)"
```

这个是定制过的，不是默认的Nginx日志格式，首先看Nginx的配置文件，搞清楚每一列是什么意思，然后按照goaccess 的约定编写配置文件，然后才能分析日志。
Nginx的配置文件里写的是
```
[$time_local],$remote_addr,$http_x_forwarded_for,$xxx,$request,$request_length,$request_time,$body_bytes_sent,$status,"$http_referer","$http_user_agent"'
```

那么大概知道每一列是干什么的了，然后根据goaccess的[配置格式要求][4],编辑`~/.goaccessrc`文件，内容为
``` plain ~/.goaccessrc
date_format [%d/%b/%Y:%H:%M:%S %z]
log_format %d,%h,%^,%^,%r,%^,%^,%b,%s,%R,%u
```
ok，然后执行`goaccess -f nginx_access.log.2012-07-27 -a > report.html` ，就可以生成html格式的报告了。
目前IE系列依然占有65%，其中IE6有20%左右。。


[1]: http://goaccess.prosoftcorp.com/
[2]: http://www.cnphp.info/goaccess-nginx-log-stat-tool-intro.html
[3]: http://goaccess.prosoftcorp.com/download
[4]: http://goaccess.prosoftcorp.com/man
