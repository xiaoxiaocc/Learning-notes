
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [JSP简介](#jsp简介)
* [常见动态网站开发技术对比](#常见动态网站开发技术对比)
* [Jsp页面元素构成](#jsp页面元素构成)
* [Jsp指令](#jsp指令)
* [Jsp注释](#jsp注释)
* [Jsp脚本](#jsp脚本)
* [Jsp声明](#jsp声明)
* [Jsp表达式](#jsp表达式)
* [Jsp生命周期](#jsp生命周期)
* [jspService()](#jspservice)
* [关于编码](#关于编码)

<!-- tocstop -->

## JSP简介
&nbsp;&nbsp;JSP全名为Java Server Pages,其根本是一个简化的Servlet设计，他实现了在Java当中使用HTML标签，JSP是一种动态网页技术标准也是JAVAEE的标准。JSP与Servlet一样，是在服务端运行的。

## 常见动态网站开发技术对比
- Jsp：Java平台，安全性高，适合开发大型的，企业级的Web应用程序。
- Asp.net：.Net平台，简单易学。但是安全性以及跨平台性差。
- Php：简单，高效，成本低开发周期短，特别适合中小型企业的Web应用开发.(LAMP:Linux+Apache+MySql+PHP)


## Jsp页面元素构成
1. 指令
2. 表达式
3. 小脚本
4. 声明
5. 注释
6. 静态内容

## Jsp指令
- page：通常位于jsp页面的顶端，同一个页面可以有多个page指令。
- include：将一个外部文件嵌入到当前的JSP文件中，同时解析这个页面中的JSP语句。
- taglib:使用标签库定义新的自定义标签，在jsp页面中启动定制行为。


## Jsp注释
1. HTML的注释：``` <!-- --> ```在客户端可见
2. Jsp的注释：<%-- --%> 客户端不可见
3. JSP脚本注释：``` // /*/ ```

## Jsp脚本
<% Java代码 %>

## Jsp声明
<!% Java代码 %>

## Jsp表达式
<% =表达式 %> 表达式不以分号结束

## Jsp生命周期
```
    用户发出请求index.jsp
    if(是第一次请求){
      Jsp引擎把该jsp文件转换成一个Servlet,生成字节码文件并执行jspInit();
    }else{
      直接访问生成的字节码文件
    }
    解析执行，jspService()
```
## jspService()
该方法被调用来处理客户端的请求。对每一个请求，JSP引擎创建一个新的线程来处理该请求。如果有多个客户端同时访问该JSP文件，则JSP引擎会创建多个线程。每个客户端请求对应一个线程。以多线程的方式执行可大大降低对系统的资源需求，提高系统的并发量及响应时间。但也要注意多线程的编程带来的同步问题，由于该Servlet始终驻于内存，所以响应是非常快的。

## 关于编码
- pageEncoding是jsp文件本身的编码。
- contentType的charset是指服务器发给客户端时的内容编码。
- contentType更常用。
