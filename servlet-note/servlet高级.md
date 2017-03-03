
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [获取初始化参数](#获取初始化参数)
* [MVC（Mode View Controller）](#mvcmode-view-controller)
* [Model2](#model2)

<!-- tocstop -->

## 获取初始化参数
在web.xml中，如下配置：
``` xml
<servlet>
        <servlet-name>GetInitParameterServlet</servlet-name>
        <servlet-class>servlet.GetInitParameterServlet</servlet-class>
        <init-param>
            <param-name>username</param-name>
            <param-value>admin</param-value>
        </init-param>
        <init-param>
            <param-name>password</param-name>
            <param-value>admin</param-value>
        </init-param>
</servlet>
```
其中```<init-param></init-param```标签之间是初始化参数的配置。然后再servlet对应的文件中，可以用```this.getInitParameter("username")```来获得。

## MVC（Mode View Controller）
它是软件开发过程中比较流行的设计思想。旨在分离模型、控制、视图。是一种分层思想的体现。
在web开发中，充当Controller角色的是Servlet,充当View角色的是JSP,充当Model的为javaBean，指定数据访问层来操作数据库，也就是dao。

## Model2
Java Web的Model2开发模型就是MVC思想的体现。
- JavaBean(M)
- Servlet(C)
- JSP(V)
- DB

具体过程如下：
1. JSP提交请求到Servlet。
2. Servlet实例化模型层的对象，或者说调用模型层（javabean）的功能。
3. 模型层访问数据库层，将得到的结构反馈给控制层（servlet）。
4. Servlet根据结果的不同，给用户呈现不同也页面，也就是跳转到不同的JSP页面。
