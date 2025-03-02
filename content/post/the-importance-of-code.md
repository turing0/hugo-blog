---
title: 写代码的重要性
tags:
  - 随笔
date: 2020-03-02 14:53:06
---

如果26个英文字母

A B C D E F G H I J K L M N O P Q R S T U V W X Y Z

<!--more-->

分别等于:

1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26

那么：

Knowledge (知识)： K+N+O+W+L+E+D+G+E＝ 11+14+15+23+12+5+4+7+5=96%

Workhard (努力工作）：W+O+R+K+H+A+R+D＝ 23+15+18+11+8+1+18+4 =98%

也就是说知识和努力工作对我们人生的影响可以达到96％和98％。

Luck（好运）： L+U+C+K＝12+21+3+11=47%。

Love（爱情）： L+O+V+E＝12+15+22+5=54%。

看来，这些我们通常认为重要的东西却并没起到最重要的作用。

那么，什么可以决定我们100％的人生呢？

是Money（金钱）吗？M+O+N+E+Y=13+15+14+5+25=72%。

看来也不是。

是Leadership (领导能力)吗？

L+E+A+D+E+R+S+H+I+P=12+5+1+4+5+18+19+9+16=89%

还不是。

金钱，权力也不能完全决定我们的生活。那是什么呢？

其实，真正能使我们生活圆满的东西就在我们的代码里面！

iostream(输入输出流所在的头文件)

I+O+S+T+R+E+A+M=9+15+19+20+18+5+1+13=100%。

所以坚持写代码吧！

没毛病😁

```python
import random
def money_val(min, max):
    return min if min > max else random.randint(min, max)
def redenvelope(money, n, min = 0.01):
    """
    :param money:   红包金额
    :param n:       抢红包的人数
    :param min:     抢到红包的最小金额
    :return:        每个人抢到红包的金额
    """
    money_list = []
    if money < n * min:
        return money_list, u'Invalid Value'
    for i in range(1, n):
        safe_total = (money - (n - i) * min) / (n - i)
        get_money = round(money_val(min * 100, int(safe_total) * 100) / 100, 2)
        money -= get_money
        money_list.append(get_money)
    money_list.append(round(money, 2))
    random.shuffle(money_list)
    return money_list, u'success'
```