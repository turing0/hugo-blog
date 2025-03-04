---
title: CTF基础 i春秋学习笔记
slug: ctf-ichunqiu-note
tags:
  - CTF
  - Note
categories:
  - Note
date: 2020-03-03 04:24:28
---

课程来源于i春秋 https://www.ichunqiu.com/course/63212

第一章 竞赛简介
--------

### 1.二进制安全学习规划指南

核心基础课程-计算机的工作原理

* 体系结构
* 编译原理
* 操作系统

<!--more-->

其他基础课程-系统软件开发基础

* 编程语言
* 网络协议
* 数据结构与算法

基础课程学习--体系结构

CPU的设计与实现

* 机器指令与汇编语言
* 指令的解码、执行
* 内存管理

CMU 18-447 Introduction to Computer Architecture

* [https://www.ece.cmu.edu/~ece447/s15/doku.php](https://www.ece.cmu.edu/~ece447/s15/doku.php)
* Labs: Implement a MIPS CPU using Verilog

编译原理的设计与实现

* 自动机、词法分析、语法分析
* 运行时
* 程序静态分析

Stanford CS143-Compilers

* [http://web.stanford.edu/class/cs143/](http://web.stanford.edu/class/cs143/)
* PA: Compilers for Cool language

基础课程学习--操作系统

操作系统的设计与实现

* 系统的加载与引导
* 用户与内核态、系统调用、中断和驱动
* 进程与内存管理、文件系统
* 虚拟机

MIT 6.828-Operating System Engineering

* [https://pdos.csail.mit.edu/6.828/2016/](https://pdos.csail.mit.edu/6.828/2016/)
* Labs: Implement jos
* Xv6, a simple Unix-like teaching operating system

CTF历史资料库：https://github.com/ctfs

Wargames

* https://pwnable.kr/
* https://smashthestack.org/

漏洞挖掘与利用实战-目标

网络协议的实现

* http/SMB/DNS/SPnp-Server

脚本列表

* javascript Engine
* ActionScript Engine
* PHP/Java Sandbox Escape

内核

* Linux/Android
* Freebsd
* Apple ios
* Sony PS4

漏洞挖掘与利用实战-准备

学习历史漏洞-CVEs

挖掘新漏洞

* 逆向分析+代码审计
  * 快速逆向与快速理解
  * 对漏洞的感觉
* 模糊测试
  * 测试框架
  * 样例生成的想法

构建系统防护-研究与探索

漏洞自动挖掘技术

* 静态程序分析
* 符号执行
* 机器学习？

漏洞利用防护机制

* Intel SGX
* 控制流完整性（CFI）
* 拟态？

### 2.Web安全学习规划指南

漏洞类型

注入类

* sql注入
* xss
* xxe
* 命令执行、命令注入
* 文件上传、文件下载

信息泄露

* 源码泄露
* 敏感信息接口
* 员工资料泄露
* 服务器信息泄露

逻辑类

* 权限绕过
* 条件竞争
* 数据篡改

基础课程学习

核心基础课程-网站工作原理

* http协议
  * http-header构成（request，response）
  * http-body构成（request，response）
  * http方法
* webserver
  * webserver分类
  * webserver解析流程
  * webserver基础安全

其他基础课程-软件开发基础

* 编程语言
  * 前端:html、js、css
  * 后端、脚本语言：php、java、python
* 数据库原理
  * 关系型数据库
  * 非关系型数据库

漏洞挖掘与利用

准备

信息收集工具

* 端口
* 子域名
* 代码泄露
* 员工字典

数据包抓取修改重放工具

顺手的浏览器以及插件

vps，漏洞验证

挖掘

分析业务功能

分析web架构

针对罗列可能的漏洞类型

详细测试：不要放过任何一个数据包

利用举例

单一利用

* getshell
* 敏感信息接口

组合利用

* xss+csrf

### 3.CTF与人才培养学习规划指南

基础课程学习

核心基础课程-相关偏向实战的课程

* Web安全
* 二进制安全
  * 逆向工程
  * 漏洞利用
* 密码学相关

其他基础课程-开发、取证、隐写等

* 编程语言
* 网络协议
* 数据结构与算法
* 取证分析

Web安全中的漏洞类型

* 注入类
  * sql注入
  * xss
  * xxe
  * 命令执行、命令注入
  * 文件上传、文件下载
* 信息泄露
  * 源码泄露
  * 敏感信息接口
  * 员工资料泄露
  * 服务器信息泄露
* 逻辑类
  * 权限绕过
  * 条件竞争
  * 数据篡改

逆向工程需要了解的知识

* 体系结构
  
  * 机器指令与汇编语言
  * ...

* 编译原理
  
  * 自动机、词法分析、语法分析
  * ...

* 操作系统
  
  * 系统的加载与引导
  * ...

漏洞利用需要了解的知识

* 逆向工程
* 模糊测试
* 什么是漏洞
* 程序员在什么时候会犯错

其他

密码学

古典密码学

* 凯撒密码
* 移位密码
* ...

现代密码学

* 对称加密体系
  * DES
  * AES
* 非对称加密体系
  * RSA

**CTF相关资料**  

CTF比赛详情:  
https://ctftime.org/  
ctf历史资料库:  
https://github.com/ctfs  
Wargames & Labs :  
http://pwnable.kr/  
http://smashthestack.org/  
http://wargame.kr/  
https://pentesterlab.com/  
http://overthewire.org/wargames/  
https://exploit-exercises.com/

END