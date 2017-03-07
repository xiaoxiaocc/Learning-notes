
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [Web应用程序](#web应用程序)
* [软件开发领域三大方向](#软件开发领域三大方向)
* [静态网页与动态网页](#静态网页与动态网页)
* [搭建Web开发环境](#搭建web开发环境)
* [Tomcat服务器的目录结构](#tomcat服务器的目录结构)
* [Tomcat WEB-INF目录](#tomcat-web-inf目录)
* [Tomcat配置默认欢迎页](#tomcat配置默认欢迎页)
* [修改Tomcat服务器的端口号](#修改tomcat服务器的端口号)

<!-- tocstop -->

## Web应用程序
web应用程序是一种可以通过web访问的应用程序。web应用程序的最大好处是用户很容易访问应用程序。用户只需要有浏览器即可，不需要再安装其他软件。



## 软件开发领域三大方向
1. 桌面应用程序：qq,office
2. Web应用程序：京东，天猫
3. 嵌入式应用程序：ios android

## 静态网页与动态网页
- 静态网页：网页中的内容固定,不会更新
- 动态网页：网页中的内容通过程序显示，自动更新。
- 所需要技术：
 - html,css,数据库
 - java or C# or php
 - XML
- 主流动态网页技术：
  - Jsp
  - Asp.net
  - Php

## 搭建Web开发环境
- JDK
- Tomcat
- Intellij idea

## Tomcat服务器的目录结构
- /bin 存放各种平台下用于启动或停止Tomcat的命令文件
- /conf存放Tomcat服务器的各种配置文件
- /lib存放Tomcat服务器所需要的各种JAR文件
- /logs 存放Tomcat的日志文件
- /temp Tomcat运行时用于存放临时文件
- /webapps 当发布Web应用时，默认会将Web应用的文件发布到此目录下
- /work Tomcat爸JSP生成的Servlet放于此目录下

## Tomcat WEB-INF目录
1. WEB-INF是Java的Web应用的安全目录。所谓安全就是客户端无法访问，只有服务端可以访问的目录。
2. web.xml 项目部署文件
3. classes文件夹，用于放置*.class文件
4. lib文件夹，用于存放需要的jar包

## Tomcat配置默认欢迎页
在web.xml文件中输入以下内容：
``` XML
  <welcome-file-list>
    <welcome-file>welcome.jsp</welcome-file>
  </welcome-file-list
```
##  修改Tomcat服务器的端口号
通过修改conf/server.xml

``` xml
<Connector port="8080"
  protocol="HTTP/1.1"
  connectionTimeout="20000"
  redirectPort="8443"
  />
```
