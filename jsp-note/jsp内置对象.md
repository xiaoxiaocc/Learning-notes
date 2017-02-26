
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [JSP内置对象](#jsp内置对象)
  * [out对象](#out对象)
  * [request对象](#request对象)
  * [response对象](#response对象)
  * [请求转发和请求重定向](#请求转发和请求重定向)
  * [session](#session)
    * [session的生命周期](#session的生命周期)
  * [session的超时时间设置](#session的超时时间设置)
  * [application对象](#application对象)
  * [page对象](#page对象)
  * [pageContext对象](#pagecontext对象)
  * [config对象](#config对象)
  * [exception对象](#exception对象)
* [form的提交方式](#form的提交方式)

<!-- tocstop -->


## JSP内置对象
JSP内置对象是Web容器创建的一组对象，不是用new关键字就可以使用的对象。

1. out
2. request
3. response
4. session
5. application
6. Page
7. pageContext
8. exception
9. config


### out对象
1. void clear():清除缓冲区的内容，如果在flush之后调用会抛出异常。
2. void clearBuffer()：清除缓冲区内容，如果在flush之后调用不会抛出异常。
3. boolean isAutoFlush()：返回缓冲区满时，是自动清空还是抛出异常。

### request对象
客户端的请求被封装在request对象中，通过它才能了解到客户的需求，然后做出响应。它是HttpServletRequest类的实例。request对象具有请求域，即完成客户端的请求之前，该对象一直有效。<br>

**request.setCharacterEncoding("utf-8") 解决中文乱码问题。但无法解决URL传递中文出现的乱码问题。如:**
```
<a href="request.jsp?" username="李四">测试URL传参数</a>
```
其解决方式是：通过修改tomcat服务器的server.xml文件，在Connector标签中添加 **URIEncoding="utf-8"**
``` xml
  <Connector port="8080" protocol="HTTP/1.1"
  connectionTimeout="20000"
  redirectPort="8843"
  URIEncoding="utf-8" />

```

### response对象
response对象包含了响应客户请求的有光信息，但在JSP中很少用到它。它是HttpServletResponse类的实例。response对象具有页面作用域，即访问一个页面时，该页面的response对象只能对这次访问有效，其他页面的response对象对当前页面无效。

- **PrintWriter getWriter()：** 返回可以向客户端输出自负的一个对象。
- **senRedirect(java.lang.Sgring location)：** 重定向客户端的请求

out对象打印的内容总在PrintWriter类的对象所打印的内容后面显示。使用out.flush()可改变这种情况。

### 请求转发和请求重定向
- 请求重定向：
  1. 客户端行为
  2. response.senRedirect()
  3. 从本质上讲等同于两次请求，前一次的请求对象不会保存，地址栏的URL地址会改变。
- 请求转发：
  1. 服务器行为
  2. request.getRequestDispatcher().forward(req,resp);
  3. 是一次请求，转发后请求对象会保存，地址栏的URL地址不会改变。
- **example:**
   1. 重定向：你先去了A句，A句的人说:"这个事不归我们管，去B局"，然后，你就从A局退了出来，自己乘车去了B局。
   2. 转发： 你去了A局，A局看了以后，知道这个事情其实应该是B局来管，但是他没有把你退回来，而是让你坐了一会儿，自己到后面办公室联系了B的人，让他们办好后，送了过来。

### session
 - session表示客户端与服务器的一次会话。
 - Web中的session指的是用户在浏览某个网站时，从进入网站到浏览器关闭所经过的这段时间，也就是用户浏览这个网站所花费的时间。
 - session实际上是一个特定的时间概念。

- session对象在第一个JSP页面被装载的时候自动创建，完成会话管理。
- 从一个客户打开浏览器并连接到服务器开始，到客户关闭浏览器离开这个服务器结束，成为一个会话。
- 当一个客户访问一个服务器时，可能在服务器的几个页面之间切换，服务器应当通过某种方法知道这是一个客户。
- session对象是HttpSession类的实例。

#### session的生命周期

- **创建:** 当客户端第一次访问某个JSP活着Servlet时，服务器会为当前会话创建一个SessionId,每次客户端向服务器发送请求时，都会此SessionId携带过去，服务端会对此SessionId进行校验，判断是否属于同一次会话。
- **活动：**
  - 某次会话中通过超链接打开的页面属于同一次会话。
  - 只要当前页面没有关闭，重新打开浏览器窗口访问同一项目资源属于同一次会话
  - 除非本次会话中所有页面都关闭后再重新访问某个JSP活着Servlet将会创建新的会话。
  - 需要注意的是：原会话还存在，只是这个旧的sessionId仍然存在于服务端，只不过再也没有客户端会携带它然后交予服务器校验。
- **销毁：**
  - 调用session.invalidate()方法。
  - session过期（超时）
  - 服务器重新启动

### session的超时时间设置
1. session.setMaxInactiveInterval（时间）; 单位：秒
2. 在web.xml配置：
``` xml
  <session-config>
    <session-timeout>
      10
    </session-timeout>
  </session-config>
```
3. Tomcat默认的session时间为30秒。

### application对象
- application对象实现了用户间数据的共享，可存放全局变量。
- application对象开始与服务器的启动，终止与服务器的关闭。
- 在用户的前后或者不同用户的连接中，可以对application对象的同一属性进行操作。
- 在任何地方对application对象属性的操作，都将影响其他用户对此的访问。
- 它是属于服务器的对象，不属于具体某个项目。服务器的启动和关闭决定了application对象的生命。
- application对象是ServletContext类的实例

### page对象
page对象是指当前的JSP页面本身，有点像类中的this指针，它是java.lang.Obejct类的实例。

### pageContext对象
- pageContext对象提供了对JSP页面内所有的对象及名字空间的访问。
- pageContext对象可以访问本页面所在的session,也可以取本页面所在的application的某一属性。
- 相当于页面中所有功能的集大成者。
- pageContext对象的本类名也叫pageContext。

### config对象
config对象是在一个Servlet初始化时，JSP引擎向它传递信息用的，此信息包括Servlet初始化时要用到的参数（由属性名和属性值构成）以及服务器的有关信息（通过传递一个ServletContext对象）。

### exception对象
如果jsp页面要应用此对象，就必须把isErroPage设为true，否则无法编译。它实际上是java.lang.Throwable的对象。
<@ page errorPage="exception.jsp">是指当前也买你发生异常时，交给哪个页面去处理。处理页面的<@ page isErrorPage="true">


## form的提交方式
1. **get**:以明文的方式通过URL提交数据，数据在URL中可以看到。提交的数据最多不超过2KB。安全性较低但效率比post方式高。适合提交数据量不大，安全性不高的数据。比如:搜索、查询等功能。
2. **post**：将用户提交的信息封装在HTML HEADER内。适合提交数据量大，安全性高的用户信息。比如：注册、修改、上传等功能。
