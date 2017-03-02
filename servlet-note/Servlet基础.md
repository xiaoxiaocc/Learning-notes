
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [Tomcat容器等级](#tomcat容器等级)
* [Servlet继承体系](#servlet继承体系)
* [手工编写Servlet](#手工编写servlet)
* [Servlet的生命周期](#servlet的生命周期)
* [Servlet对象与九大内置对象之间的对应关系](#servlet对象与九大内置对象之间的对应关系)
* [servlet的绝对路径与相对路径](#servlet的绝对路径与相对路径)

<!-- tocstop -->

## Tomcat容器等级
Tomcat容器分为4个等级，Servlet的容器管理Context容器，一个Context对应一个Web工程。具体包含情况如下：

- Tomcat
  - Container
    - Engine
      - Host
        - Servlet
          - Context

从上到下为包含关系。

## Servlet继承体系

- Servlet（itnerface）
  - GenericServlet(Abstract Class)
    - HttpServlet(Abstract Class)
      - 自定义Servlet

- Servlet接口包含三个接口:
 ``` Java
Init(),Service(),destroy()
```
- GenericServlet是与协议无关的Servlet。
- HttpServlet是实现了http协议的Servlet。
- 对于自定义的Servlet，一般是继承HttpServlet,重写```doGet()```与```doPost()```方法。

## 手工编写Servlet

1. 继承HttpServlet
2. 重写```doGet()```或者```doPost()```方法
3. 在web.xml中注册Servlet
4. 一般的IDE都有直接创建Servlet的选项
5. 在```doGet()```或者```doPost()```方法中，可以指定输出的文件类型，这样就可以在网页中输出html代码。如下：
``` Java
  response.setContentType("text/html;charset=utf-8");

  然后，如下代码就可以使输出的内容被浏览器解析为html代码。

  PrintWriter out = response.getWriter();
  out.println("<strong>Hello Servlet!</strong><bt>");
```

## Servlet的生命周期
servlet是长期驻留在内存的，在下列时刻Servlet容器装载Servlet:

1. Servlet容器启动时自动装载某些Servlet,实现它只需要在web.xml文件中的```<servlet></servlet>```之间添加如下代码：```<loadon-startup>1</loadon-startup>```,数字越小表示优先级别越高。

2. 在Servlet容器启动后，客户端首次向Servlet发送请求。
3. Servlet类文件被跟新后，重新装载Servlet。

servlet在被装载后，servlet容器创建一个servlet实例并且调用servlet的```inite()```方法进行初始化，在Servlet的整个生命周期内，init()方法只被调用一次。

## Servlet对象与九大内置对象之间的对应关系

| JSP对象 | 怎样获得
--- | ---
out | resp.getWriter
request | service方法中的req参数
response | service方法中的resp
session | req.getSession()函数
application | getServletContext()函数
exception | Throwable
page | this
pageContext | PageContext
Config | getServletConfig函数

## servlet的绝对路径与相对路径
- 在配置```<servlet-mapping></servlet-mapping>``` 的时候,
``` Xml
 <url-pattern>/servlet/LoginServlet</url-pattern>
```
servlet前面要加根号，否则服务器无法启动。其中servlet是包名，LoginServlet是servlet对应的文件。

- 获取项目的根路径：
``` Java
request.getContextPath();
```
- 一般 ```/```要么代表服务器的根路径，要么代表项目的根路径。在无法确定的时候，自己可以都试试加或者不加。如果使用绝对路径的话。
- 也可以使用绝对路径，用```getContextPath()```函数获取项目根目录的路径，然后再加上其他的。
