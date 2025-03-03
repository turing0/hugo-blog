---
title: 数据结构与算法 学习笔记
date: 2020-03-25 23:51:34
tags: [算法,数据结构,Datastruct,Algorithm]
categories: 
  - Algorithms
---

笔记略长， 排版略丑

serendipity

# 数据结构与算法总览

## 分解数据结构和算法

数据结构

<!--more-->

- 一维
  
  - 基础：数组 array(string),链表 linked list
  - 高级：栈 stack,队列 queue，双端队列 deque，集合 set，映射 map(hash or map),etc

- 二维
  
  - 基础：树 tree，图 graph
  - 高级：二叉搜索树 binary search tree (red-black tree, AVL),堆 heap，并查集 disjoint set，字典树 Trie,etc

- 特殊
  
  - 位运算 Bitwise, 布隆过滤器 BloomFilter 
  - LRU Cache

注意：了解每个数据结构的原理和代码框架

### 算法

- If-else, switch —> branch 
- for, while loop —> Iteration
- 递归 Recursion (Divide & Conquer, Backtrace) 
- 搜索 Search: 深度优先搜索 Depth first search, 广度优先搜索 Breadth first search, A*, etc
- 动态规划 Dynamic Programming
- 二分查找 Binary Search
- 贪心 Greedy
- 数学 Math , 几何 Geometry

注意：在头脑中回忆上面每种算法的思想和代码模板

### 算法脑图

https://www.edrawsoft.cn/viewer/public/s/05f47326887492

https://naotu.baidu.com/file/0a53d3a5343bd86375f348b2831d3610?token=5ab1de1c90d5f3ec

### 数据结构脑图

https://www.edrawsoft.cn/viewer/public/s/d2bd7352481144

https://naotu.baidu.com/file/b832f043e2ead159d584cca4efb19703?token=7a6a56eb2630548c

## 五步刷题法

### 刷题第一遍

- 5分钟：读题 + 思考 
- 直接看解法：注意！多解法，比较解法优劣
- 背诵、默写好的解法

### 刷题第二遍

- 马上自己写 —> LeetCode 提交
- 多种解法比较、体会 —> 优化！

### 刷题第三遍

- 过了一天后，再重复做
- 不同解法的熟练程度 —> 专项练习

### 刷题第四遍

- 过了一周：反复回来练习相同题目

### 刷题第五遍

- 面试前一周恢复性训练

---

# 训练准备

## 训练环境设置、编码技巧和Code Style

### 电脑设置

- Google
- Mac: iTerm2 + zsh (oh my zsh)Windows: 
  Microsoft new terminal: (https://github.com/microsoft/terminal)
- VSCode; Java: IntelliJ; Python: Pycharm
- LeetCode plugin (VSCode & IntelliJ)
- https://vscodethemes.com
- 骚操作：
  - https://juejin.im/post/5ce1365151882525ff28ed47

### Code Style

Java、 Python、...

- Google code style
- Facebook
- airbnb

### LeetCode

- leetcode-cn.com 和题解
- leetcode.com 和 Discuss board

### 指法和小操作

- home, end 或 fn + ⬅➡（行头、行尾）
- Ctrl + ⬅➡ （到左右的下一词）
- Ctrl + backspace （删除词）
- IDE 的⾃自动补全
- Top tips for < IDE - name>

### 自顶向下的编程方式

- https://markhneedham.com/blog/2008/09/15/clean-code-book-review/
- https://leetcode-cn.com/problems/valid-palindrome/

# 复杂度分析

如何理解算法时间复杂度的表示法，例如 O(n²)、O(n)、O(1)、O(nlogn) 等？

https://www.zhihu.com/question/21387264

Master theorem

https://en.wikipedia.org/wiki/Master_theorem_(analysis_of_algorithms)

主定理

http://zh.wikipedia.org/wiki/

## 大O复杂度表示法

所有代码的执行时间T(n)与每行代码的执行次数n成正比,即大O。
$$
T(n) = O(f(n))
$$
其中，T(n)表示代码执行的时间；n表示数据规模的大小；f(n)表示每行代码执行的次数总和。因为这是一个公式，所以用f(n)来表示。公式中的O，表示代码的执行时间T(n)与f(n)表达式成正比。

大O时间复杂度实际上并不具体表示代码真正的执行时间，而是表示代码执行时间随数据规模增长的变化趋势，所以，也叫作渐进时间复杂度（asymptotic time complexity），简称时间复杂度。

- 如何分析一段代码的时间复杂度？
  
  1. 只关注循环执行次数最多的一段代码
     大O这种复杂度表示方法只是表示一种变化趋势。我们通常会忽略掉公式中的常量、低阶、系数，只需要记录一个最大阶的量级就可以了。所以，我们在分析一个算法、一段代码的时间复杂度的时候，也只关注循环执行次数最多的那一段代码就可以了。这段核心代码执行次数的n的量级，就是整段要分析代码的时间复杂度。
     
     ```c++
     int cal(int n) {   
         int sum = 0;   
         int i = 1;   
         for (; i <= n; ++i) {     
             sum = sum + i;   
         }   
         return sum; 
     }
     ```
     
     其中第2、3行代码都是常量级的执行时间，与n的大小无关，所以对于复杂度并没有影响。循环执行次数最多的是第4、5行代码，所以这块代码要重点分析。前面我们也讲过，这两行代码被执行了n次，所以总的时间复杂度就是O(n)
  
  2. 加法法则：总复杂度等于量级最大的那段代码的复杂度
     
     ```c++
     int cal(int n) {
         int sum_1 = 0;
         int p = 1;
         for (; p < 100; ++p) {     
             sum_1 = sum_1 + p;   
         }   
         int sum_2 = 0;   
         int q = 1;
         for (; q < n; ++q) {     
             sum_2 = sum_2 + q;   
         }   
         int sum_3 = 0;   
         int i = 1;   
         int j = 1;   
         for (; i <= n; ++i) {     
             j = 1;      
             for (; j <= n; ++j) {       
                 sum_3 = sum_3 +  i * j;     
             }   
         }   
         return sum_1 + sum_2 + sum_3; 
     }
     ```
     
     这个代码分为三部分，分别是求sum_1、sum_2、sum_3。我们可以分别分析每一部分的时间复杂度，然后把它们放到一块儿，再取一个量级最大的作为整段代码的复杂度。第一段的时间复杂度是多少呢？这段代码循环执行了100次，所以是一个常量的执行时间，跟n的规模无关。
     
     这里我要再强调一下，即便这段代码循环10000次、100000次，只要是一个已知的数，跟n无关，照样也是常量级的执行时间。当n无限大的时候，就可以忽略。尽管对代码的执行时间会有很大影响，但是回到时间复杂度的概念来说，它表示的是一个算法执行效率与数据规模增长的变化趋势，所以不管常量的执行时间多大，我们都可以忽略掉。因为它本身对增长趋势并没有影响。
     
     那第二段代码和第三段代码的时间复杂度是多少呢？答案是O(n)和O(n2)
     
     综合这三段代码的时间复杂度，我们取其中最大的量级。所以，整段代码的时间复杂度就为O(n2)。也就是说：总的时间复杂度就等于量级最大的那段代码的时间复杂度。
  
  3. 乘法法则：嵌套代码的复杂度等于嵌套内外代码复杂度的乘积
     
     ```c++
     int cal(int n) {   
         int ret = 0;    
         int i = 1;   
         for (; i < n; ++i) {     
             ret = ret + f(i);   
         }  
     }  
     int f(int n) {  
         int sum = 0;  
         int i = 1;  
         for (; i < n; ++i) {    
             sum = sum + i;  
         }   
         return sum; 
     }
     ```
     
     单独看cal()函数。假设f()只是一个普通的操作，那第4～6行的时间复杂度就是，T1(n) = O(n)。但f()函数本身不是一个简单的操作，它的时间复杂度是T2(n) =O(n)，所以，整个cal()函数的时间复杂度就是，T(n) = T1(n) * T2(n) = O(n*n) = O(n2)。

O(1):  Constant Complexity 常数复杂度

O(log n):  Logarithmic Complexity 对数复杂度

- ```c++
  i=1; 
  while (i <= n)  {   
      i = i * 2; 
  }
  ```
  
  这段代码的时间复杂度就是O(log2n)
  
  ```c++
  i=1; 
  while (i <= n)  {   
      i = i * 3; 
  }
  ```
  
  这段代码的时间复杂度为O(log3n)

  实际上，不管是以2为底、以3为底，还是以10为底，我们可以把所有对数阶的时间复杂度都记为O(logn)。为什么呢？

  我们知道，对数之间是可以互相转换的，log3n就等于log32 * log2n，所以O(log3n) = O(C * log2n)，其中C=log32是一个常量。基于我们前面的一个理论：在采用大O标记复杂度的时候，可以忽略系数，即O(Cf(n)) = O(f(n))。所以，O(log2n) 就等于O(log3n)。因此，在对数阶时间复杂度的表示方法里，我们忽略对数的“底”，统一表示为O(logn)。

- 如果一段代码的时间复杂度是O(logn)，我们循环执行n遍，时间复杂度就是O(nlogn)了。而且，O(nlogn)也是一种非常常见的算法时间复杂度。比如，归并排序、快速排序的时间复杂度都是O(nlogn)。

O(n):  Linear Complexity 线性时间复杂度

O(n^2): N square Complexity 平方

O(n^3): N square Complexity 立方

O(2^n): Exponential Growth 指数

O(n!): Factorial 阶乘

注意：只看最⾼高复杂度的运算

O(k^n)

int fib(int n) {

​     if (n <= 2) return n;     return fib(n - 1) + fib(n - 2); }

⼆叉树遍历 - 前序、中序、后序：O(N)

图的遍历：O(N)

搜索算法：DFS、BFS - O(N)

二分查找：O(logN)

# 以下为邓俊辉老师数据结构与算法的笔记

冒泡排序

第一次看到这么写的， 刚开始还有点没看懂

```c++
void bubblesort(int a[],int n){
    for (bool sorted = false; sorted = !sorted; n--){
        for (int i = 1; i < n; i++){
            if (a[i-1] > a[i]){
                int t=a[i-1];
                a[i-1] = a[i];
                a[i] = t;
                sorted = false;
            }
        }
    }
}
```

求数组中 最大的两个数的下标  [lo ,hi)

递归 + 分治

```c++
void max2(int a[],int lo,int hi,int &x1,int &x2){
    if (lo + 2 == hi){
        if (a[lo] >= a[lo+1]){
            x1 = lo;
            x2 = lo+1;
        }
        else {
            x2 = lo;
            x1 = lo+1;
        }
        return ;
    }
    if (lo + 3 == hi){
        if (a[x1 = lo] < a[x2 = lo+1]) swap(x1,x2);
        if (a[lo+2] > a[x2]){
            if (a[x2 = lo+2] > a[x1]){
                swap(x1,x2);
            }
        }
        return ;
    }
    int mi = (lo + hi)/2;
    int x1l,x2l;max2(a,lo,mi,x1l,x2l);
    int x1r,x2r;max2(a,mi,hi,x1r,x2r);

    if (a[x1l] > a[x1r]){
        x1 = x1l;
        x2 = a[x2l] > a[x1r] ? x2l:x1r;
    }
    else{
        x1 = x1r;
        x2 = a[x1l] > a[x2r] ? x1l:x2r;
    }
    return ;
}
```

斐波那契数列、FIB()回归迭代

- 解决方法A（记忆：memoization）

- ​    将已计算过的实例的结果制表查询

- 解决方法B（动态规划：Dynamic Programming）
  
  - ​    颠倒计算方向：由自顶向下递归，为自底而上迭代
    
    ```c++
    f = 0; g = 1; //fib(0), fib(1)
    while (0 < n--){
        g = g + f;
        f = g - f;
    }
    return g;
    ```
    
    T(n)=O(n), 仅需O(1)空间！
    
    ![fib-ex](https://turing0.github.io/html/img/fib-ex.png)
