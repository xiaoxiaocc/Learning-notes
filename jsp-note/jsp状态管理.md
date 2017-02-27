
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [http协议的无状态性](#http协议的无状态性)
* [保存用户状态的两大机制](#保存用户状态的两大机制)
  * [Cookie的作用](#cookie的作用)
  * [Jsp创建与使用Cookie](#jsp创建与使用cookie)
  * [session与Cookie的对比](#session与cookie的对比)
  * [进行转码](#进行转码)

<!-- tocstop -->

## http协议的无状态性

无状态是指，当浏览器发送请求给服务器的时候，服务器相应客户端请求。但是当同一个浏览器再次发送请求给服务器的时候，服务器并不知道它就是刚才那个浏览器。简单地说，就是服务器不会去记得你，所以是是无状态协议。

## 保存用户状态的两大机制
- Session
- Cookie: 是Web服务器保存在客户端的一系列文本信息。

### Cookie的作用
- 对特定对象的追踪
- 保存用户网页浏览记录与习惯
- 简化登录

安全风险：容易泄露用户信息

### Jsp创建与使用Cookie
- 创建Cookie对象：
``` Java
Cookie newCookie = new Cookie(String key,Object value);
```
- 写入Cookie对象
``` Java
response.addCookie(newCookie);
```
- 读取Cookie对象
``` Java
Cookie[] cookies = request.getCookies();
```

### session与Cookie的对比

- session:
  - 在服务器端保存用户信息
  - session中保存的是Object类型
  - 随着会话的结束而将其存储的数据销毁
  - 保存重要的信息
- cookie
  - 在客户端保存用户信息
  - cookie保存的是string 类型
  - cookie可以长期的保存在客户端
  - 保存不重要的用户信息

### 进行转码
在保存cookie字符串的时候，如果出现中文字符串的话，如果没有进行字符编码的转码的话，会抛出异常。
解决方案：
- 编码：
``` Java
String username = URLEncoder.encode(request.getParameter("username"), "utf-8");

Cookie usernameCookie = new Cookie("username", username);

response.addCookie(usernameCookie);
```
- 解码：
``` Java
 username = URLDecoder.decode(usernameCookie.getValue(), "utf-8");

 Cookie[] cookies = request.getCookies();
```
