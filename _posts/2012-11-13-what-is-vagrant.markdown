---
layout: post
title: 虚拟开发环境搭建工具vagrant介绍
date: 2012-11-13 20:16
comments: true
categories: program
---


## 介绍
vagrant是一个创建和分发虚拟化开发环境的工具，使用ruby编写，基于Oracle的VirtualBox，它提供了一个可配置的、轻量级的、可重用的、便携的虚拟化开发环境。  
类似工具的需求比如:

* 需要纯净的开发或者测试环境
* 新员工加入，需要从头搭建完整的开发环境

有了vagrant，只需要创建一个打包好的package，里面开发工具，代码库，服务器等都已经安装配置好了，需要的时候直接拿来就可以工作了。

## 使用
### 下载安装

* [下载vagrant](http://downloads.vagrantup.com)，目前的最新版本是1.0.5，vagrant可以在多个平台运行，下载自己需要的那个平台即可。需要注意的是，如果你已经安装了ruby和gem，那么直接在终端执行`gem install vagrant`即可安装vagrant。
* [下载VirtualBox](https://www.virtualbox.org/wiki/Downloads)，vagrant基于VirtualBox，所以需要安装，VirtualBox也是跨平台软件，按需下载即可。

### 创建一个box
box就相当于是一个环境，它一般是一个VirtualBox虚拟机的镜像，官方提供了一个基于Ubuntu 10.04的box。
给vagrant添加一个box:

```
vagrant box add lucid32 http://files.vagrantup.com/lucid32.box
```
其中`lucid32`表示给这个box起名lucid32。  
如果网速太慢，那么可以先用下载工具把`lucid32.box`下载过来，然后直接执行

```
vagrant box add lucid32 lucid32.box

```
即可。  
[这个网站](http://www.vagrantbox.es/)上收集了很多用户自己创建的box，可以根据自己的需要选择下载。
### 创建一个虚拟机
执行

```
vagrant init lucid32
```

表示基于lucid32创建一个虚拟环境，命令执行后会在当前目录下生成一个`Vagrantfile`文件，这个就是当前虚拟环境的配置文件，里面的内容相当于是一个ruby程序，里面的注释写的都很详细，这里就不一一介绍了。  
然后执行

```
vagrant up
```
即可启动虚拟机，默认是没有启动界面的，可以修改上面提到的配置文件使其启动时显示GUI界面。  
非windows系统在虚拟机启动后执行

```
vagrant ssh
```
即可ssh到虚拟环境中，然后就可以做自己的事了。windows系统上没有自带ssh，需要使用第三方ssh客户端，比如SecureCRT 根据`vagrant up`命令的日志也可以ssh到虚拟机中，这里就不再介绍了。。  

`Vagrantfile` 有几项比较重要的配置，这里简单介绍一下:

```
config.vm.network # 配置虚拟机网络连接方式，是否可以访问外网等
config.vm.forward_port # 配置虚拟机端口转发，比如虚拟机里服务器的端口为80，可以转发为主机的8080端口
config.vm.share_folder # 配置文件夹共享目录
puppet 和 chef  # 这两个是自动化服务器配置的，下次会单独介绍
```

### 打包box
当虚拟机里环境搭建好以后，可能需要把当前的状态打个包，分发给其他同事或者做个备份，这时执行

```
vagrant package
```
即可在当前目录生成一个`package.box`的box，这个box和前面的那个`lucid32.box`类似，你可以把它保存到其他位置作为备份了。

### 其他命令

```
vagrant halt     # 关闭虚拟机
vagrant suspend  # 休眠虚拟机
vagrant reload   # 重启虚拟机
vagrant status   # 查看当前虚拟机状态 
```
更多其他命令可以通过`vagrant help`查看。

### reference

* <http://railscasts.com/episodes/292-virtual-machines-with-vagrant>
* <http://saberma.me/linux/2011/03/03/vagrant-virtual-develop-enviroment.html>



