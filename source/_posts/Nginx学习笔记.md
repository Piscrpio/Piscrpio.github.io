---
title: Nginx学习笔记
date: 2018-05-09 13:38:36
categories: web
tags: [nginx,前端跨域]
---
### 前言
nginx：反向代理、负载均衡、指定文件（404.html）
<!--more-->
### 一、安装
[官网下载](http://nginx.org/en/download.html).建议下载最新稳定版本【Stable version】，下载完成后直接解压到某个文件夹（自己能找到）。

### 二、常用命令
```
//查看帮助
./nginx -h

//启动nginx服务，找到nginx.exe所在目录
./nginx.exe
start nginx

//停止nginx服务
./nginx -s stop  //快速停止nginx，可能并不保存相关信息
./nginx -s quit  //完整有序的停止nginx，并保存相关信息

//重启nginx服务，改变了nginx配置信息并需要重新载入这些配置时可以使用此命令重载nginx
./nginx -s reload

//查看nginx版本信息
./nginx -v  //简单显示nginx的版本信息(nginx version)
./nginx -V  //不但显示nginx的版本信息，而且还显示nginx的配置参数信息。

//重新打开日志文件命令
./nginx -s reopen


配置文件语法检查并重新加载
nginx -t && nginx -s reload
```
