# Servlet的request对象和response对象

## request对象

作用：request对象中封存了当前请求的所有请求信息

使用：

-   获取请求头数据
-   获取请求行数据
-   获取用户数据

注意：该对象由Tomcat服务器创建，并作为实参传递给处理请求的Servlet的service方法。

### 获取请求头数据

-   获取请求方式

    req.getMethod(); --->GET

-   获取请求URL和URI

    req.getRequestURL(); --->http://localhost:8080/myServlet1/myReq

    req.getRequestURI(); --->/myServlet1/myReq

-   获取协议

    req.getScheme(); --->http

    req.getServerName(); --->localhost

    req.getServerPort(); --->8080

### 获取请求行数据

-   获取单个的请求行数据

    req.getHeader("headName")

-   获取所有的请求行数据

    Enumeration<String> en = req.getHeaderNames();

    使用en.hasMoreElements()判断是否有下个枚举

    使用en.nextElement()获取下个枚举

### 获取用户数据

-   req.getParameter("键名")

    返回指定的用户数据

-   req.getParameterValues("键名")

    返回同键不同值的请求数据（多选），返回数组

-   req.getParameterNames()

    返回所有用户请求数据的枚举集合

### 多个Servlet之间传递数据

-   req.setAttribute(name,value);
-   req.getAttribute(name);

### 注意

如果要获取的请求数据不存在，不会报错，返回Null。



## response对象

作用：用来响应数据到浏览器的一个对象

使用：

-   设置响应头
-   设置响应状态码
-   设置响应编码格式
-   设置响应实体

### 设置响应头

-   resp.setHeader(key，alue)

    设置响应头，但是只能存在一个相同的key

-   resp.addHeader(key，alue)

    设置响应头，可以同时存在多个相同的key

### 设置响应状态码

-   resp.sendError(状态码,"报错信息")

    设置响应状态码，并设置和发送报错信息。

    该方法是相当于手动设置报错，其实浏览器访问是没有问题的，只不过我们不想让人访问到，所以给浏览器一个错误信息。

### 设置响应编码格式

-   resp.setHeader("content-type","text/html;charset=utf-8")

    让浏览器以何种编码方式解析Tomcat发送过去的数据

-   resp.setContentType("text/html;charset=utf-8")

    效果同上。 

### 设置响应实体

-   resp.getWriter().write("信息")

## 总结

service请求处理代码流程：

-   设置相应编码格式
-   获取请求数据
-   处理请求数据
    -   数据库操作（MVC思想）
-   响应处理结果