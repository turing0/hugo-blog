---
title: C++学习
abbrlink: cpp-study
date: 2020-05-21 17:08:00
tags: [C++,Note]
categories: Code
---

记录c++的学习

<!--more-->

# ios::sync_with_stdio(false)提高C++读写速度

C++为了兼容C，默认使iostream与stdio关联，使cin与scanf、cout和printf保持同步，保证混用过程中文件指针不混乱。
 此方式会造成性能损失，导致使用cin/cout效率远远低于使用scanf/printf。若保证程序只是用一套指令，可取消同步：

```c++
std::ios::sync_with_stdio(false);
```

取消后使用cin/cout速度有明显提升，但注意不要混用iostream与stdio（玄学）

```c++
std::cin.tie(0);
```

> C++98：In terms of *static initialization order*, cin is guaranteed to be properly constructed and initialized no later than the first time an object of type [ios_base::Init](http://www.cplusplus.com/ios_base::Init) is constructed.
> 
> C++11：In terms of *static initialization order*, cin is guaranteed to be properly constructed and initialized no later than the first time an object of type [ios_base::Init](http://www.cplusplus.com/ios_base::Init) is constructed, with the inclusion of [](http://www.cplusplus.com/) counting as at least one initialization of such objects with *static duration*.
> 
> cin is *[tied](http://www.cplusplus.com/ios::tie)* to the standard output stream [cout](http://www.cplusplus.com/cout) (see [ios::tie](http://www.cplusplus.com/ios::tie)), which indicates that [cout](http://www.cplusplus.com/cout)‘s buffer is *flushed* (see [ostream::flush](http://www.cplusplus.com/ostream::flush)) before each i/o operation performed on cin.
> 
> (来源:http://www.cplusplus.com/reference/iostream/cin/ [网址](http://网址))

当传入参数为0时，实现cin与cout独立运行，不会等待，提高cin速度

全局域的通过静态常量初始化一个lambda的方式实现对此代码的优先调用

```c++
static const int _ = []() {
    ios::sync_with_stdio(false);//ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
    cin.tie(nullptr);
    cout.tie(nullptr);
    return 0;
}();
```

**Ref**:

原文:[ios::sync_with_stdio(false)提高C++读写速度](https://www.coologic.cn/2017/11/275/)

# 自定义sort函数中的比较函数

c++ sort的官方文档
http://www.cplusplus.com/reference/algorithm/sort/

可以看到comp的定义：comp函数返回一个bool类型的值，这个值表示了在严格弱排序中（可以理解为升序排序）第一参数是否位于第二个参数之前。 
 也就是说如果comp返回true，则第一个参数小于第二个参数，sort根据compare的返回值将第一个参数排在第二个参数之前。 
 如果comp返回false，则第一个参数大于第二个参数，sort根据compare的返回值将第一个参数排在第二个参数之后。

 **sort函数根据comp函数的返回值，对comp函数的两个参数排序。** 
 **如果comp返回true，排序为“参数1”“参数2”，否则排序为“参数2”“参数1”。** 

例如降序排列，则return a>b;
