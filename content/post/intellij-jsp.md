---
title: Intellij IDEA 2020 创建 Jsp页面 及 示例
slug: intellij-jsp
date: 2021-03-14 15:12:36
tags: [Java]
categories: Code

---

Intellij 配置Tomcat, Jsp 示例。

<!--more-->

环境：Intellij idea 2020。

超详细的教程

# 创建 Servlet 步骤

新建项目

![jsp-1.png](https://i.loli.net/2021/03/28/wdCpDyb638HKsLZ.png)

选择java

![jsp-2.png](https://i.loli.net/2021/03/28/t23VulinA6ZpmzX.png)

然后next，再next

设置项目名称，点击finish

![jsp-3.png](https://i.loli.net/2021/03/28/laoENin8Ug4rFRX.png)

右键项目，添加框架支持

![jsp-4.png](https://i.loli.net/2021/03/28/jktEu5cKVYNTDes.png)

选择web application，勾选create web.xml，点击ok

![jsp-5.png](https://i.loli.net/2021/03/28/CPxYmL2bdjXZJye.png)

之后会看到如图所示文件结构

![jsp-6.png](https://i.loli.net/2021/03/28/QKJwhGUm5Axtzcl.png)

在 web-inf 文件夹下创建classes和lib文件夹

![jsp-7.png](https://i.loli.net/2021/03/28/Jvo9XQ6VyRM57Dt.png)

如图打开project structure

![jsp-8.png](https://i.loli.net/2021/03/28/J4YamtFLR6W1ncv.png)

设置成这样

![jsp-9.png](https://i.loli.net/2021/03/28/1KmpCgsLiMoBwEx.png)

按如下导入tomcat目录下servlet.jar包

![jsp-12.png](https://i.loli.net/2021/03/28/ztkxJXAHdKTuoL6.png)

![jsp-13.png](https://i.loli.net/2021/03/28/dS3AmNihlzHsDBG.png)

点击add configurations

![jsp-10.png](https://i.loli.net/2021/03/28/71WYdAIDOS8XbLR.png)

选择 tomcat server，local

![jsp-11.png](https://i.loli.net/2021/03/28/nPhgme5D3oXONCf.png)

点击fix，再点ok

![jsp-14.png](https://i.loli.net/2021/03/28/rmRiQaS74VWp15K.png)

src右键，创建 Servlet

![jsp-15.png](https://i.loli.net/2021/03/28/aTnDtO8YbZUELVs.png)

![jsp-16.png](https://i.loli.net/2021/03/28/v4MKgTcqukr8p1O.png)

# 简单的计算器示例

index.jsp 编写如下

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>Web Calculater</title>
  </head>
  <body>
    <h1>Web Calculater</h1>
    <form action="cal" method="post">
      <p>
        Input number A <input type="nubmer" name="a">
      </p>
      <p>
        Input number B <input type="nubmer" name="b">
      </p>
      <p>
        <input type="submit" value="RUN">
      </p>

    </form>
  </body>
</html>
```

calculator.java如下

```java
package com.calculator;

import jakarta.servlet.*;
import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.*;

import javax.jws.WebService;
import java.io.IOException;

@WebServlet("/cal")
public class calculator extends HttpServlet {
//    @Override
//    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
//
//    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        int a = Integer.parseInt(request.getParameter("a"));
        int b = Integer.parseInt(request.getParameter("b"));

        int sum = (a + b);
        response.getWriter().println("Sum of " + a + " and " + b + " is " + sum);
    }
}
```

启动服务可以看到

![jsp-17.png](https://i.loli.net/2021/03/28/XnrwhQagS4tTZAe.png)

随便输入几个数字即可看到成功计算

![jsp-18.png](https://i.loli.net/2021/03/28/gPS5zwDxResI9Kp.png)

可按如下设置即可实现修改jsp页面和后端数据后，刷新页面实时更新

![jsp-19.png](https://i.loli.net/2021/03/28/V6PQox7UYHZaDqg.png)

Ref:

https://cloud.tencent.com/developer/article/1633875