## include指令

``` Jsp
<%@ include file="URL" %>
```
## include动作
``` Jsp
<jsp:include page="URL" flush="true" />

flush:被包含的页面是否从缓冲区读取
```
比较内容  | include指令  | jsp:include动作   
--|---|--
语法形式  | <%@ include file="..." %>  |<jsp:include page="..."  />  
  发生作用的时间| 页面转换期间  | 请求期间  
  包含的内容|文件的实际内容（页面的源代码）   | 页面的输出
  抓换成的Servlet| 主页面和包含页面转换为一个Servlet  | 主页面和包含的页面转换为独立的Servlet
  编译时间| 较慢-资源必须被解析  | 较快
  执行时间| 稍快   | 稍慢-每次资源必须被解析

## forward动作
``` Jsp
<jsp:forward page="URL" />
等价与：
request.getRequestDispatcher("/url").forward(request,response);
```
## param动作
``` Jsp
<jsp:param name="参数名" value="参数值" />;

常常与<jsp:forward> 一起使用，作为其子标签。
可以添加新的参数，也可以修改原有的参数。
```
