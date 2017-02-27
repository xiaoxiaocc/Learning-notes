
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [Javabean是什么](#javabean是什么)
* [Javabean的设计原则](#javabean的设计原则)
* [Jsp动作元素](#jsp动作元素)
* [Jsp动作元素第一类（与存取javabeans有关的）](#jsp动作元素第一类与存取javabeans有关的)
* [给javabean对象赋值](#给javabean对象赋值)
* [Javabean的四个作用域范围](#javabean的四个作用域范围)
* [javavean对象的获取](#javavean对象的获取)

<!-- tocstop -->

## Javabean是什么
Javabean就是符合某种特定的规范的Java类。使用Javabean的好处是解决代码重复编写，减少代码冗余，功能区分明确，提高了代码的维护性。

## Javabean的设计原则
- 公有类
- 无参的公有构造方法
- 属性私有
- getter和setter方法

如：
``` Java
public class Users {
    private String username;
    private String password;
    public Users() {
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->
<!-- tocstop -->

    }
    public String getUsername() {
        return username;
    }
    public void setUsername(String username) {
        this.username = username;
    }
    public String getPassword() {
        return password;
    }
    public void setPassword(String password) {
        this.password = password;
    }
}
```
## Jsp动作元素
Jsp动作元素(action elements),动作元素为请求处理阶段提供信息。动作元素遵循XML元素的语法，有一个包含元素名的开始标签，可以有属性，可选的内容，与开始标签匹配的结束标签。

## Jsp动作元素第一类（与存取javabeans有关的）
<jsp:useBean> <jsp:setProperty> <jsp:getProperty>

## 给javabean对象赋值

1. 跟表单关联
    ``` Jsp
    <%--根据表单自动匹配所有属性--%>
        <jsp:setProperty name="myUsers" property="*"/>
    ```
2. 跟表单部分关联
    ``` Jsp
     <jsp:setProperty name="myUsers" property="username"/>
    ```
3. 手动赋值给属性
    ``` Jsp
    <jsp:setProperty name="myUsers" property="username" value="lisi"/>
        <jsp:setProperty name="myUsers" property="password" value="888888"/>
    ```
4. 跟request参数关联
    ``` Jsp
    <!--通过URL传参数给属性赋值 -->
       <jsp:setProperty name="myUsers" property="username"/>
       <jsp:setProperty name="myUsers" property="password" param="mypass"/>
    ```

## Javabean的四个作用域范围
使用useBean的scope属性来指定
1. page: 仅在当前页面有效。
2. request：仅在该请求有效。
3. session：仅在该会话有效
4. application：在此application中有效。


## javavean对象的获取
1. 使用useBean
``` Jsp
<jsp:useBean id="myUsers" class="com.po.Users" scope="page"/>
其中id就是获取到的对象的引用。
```
2. 使用内置对象
``` Jsp
<% ((Users)application.getAttribute("myUsers")).getUsername();%><br>
<% ((Users)application.getAttribute("myUsers")).getPassword();%>
<%=((Users)session.getAttribute("myUsers")).getUsername()%><br>
<%=((Users)session.getAttribute("myUsers")).getPassword() %><br>

用户：<%=((Users)request.getAttribute("myUsers")).getUsername()%><br>
密码：<%=((Users)request.getAttribute("myUsers")).getPassword() %>

```
