## Servlet（jsp）转发和重定向

### 请求转发

说明：所谓转发，就是一个Servlet处理不了完整的请求（处理一部分），接着让其他的Servlet进行处理的一种机制。

作用：实现多个Servlet联动操作处理请求，这样避免代码冗余，让Servlet的职责更加明确。

使用：

​	`req.getRequestDispatcher("要转发的地址").forward(req,resp);`

​	地址：相对地址，直接写Servlet的别名即可。

特点：一次请求，浏览器的地址栏信息不变。

使用场景：

-   因为浏览器发送请求后的地址栏信息不变，所以在处理一些不是很核心的请求时可以使用请求转发的方式。
-   若是核心的请求，就不能使用转发方式，比如转账业务，如果使用的是转发的方式，由于地址栏信息不变，每次刷新就相对于转账一次，这就行不好了。



#### 多个Servlet之间数据传递

使用request对象的 `Attribute` 属性来引用在多个Servlet之间传数据，如在AServlet中自定义的一个属性 `name=test，value=18` ，在Bservlet中获取属性名为test的值：

req.setAttribute("test","18")；

req.getAttribute("test")



### 请求重定向

说明：解决了表单重复提交的问题，以及当前Servlet无法处理的请求的问题

使用：

-   resp.sendRedirect(String uri)
-   实例：resp.sendRedirect("localhost:80/project/test")

特点：

-   两次请求，两个request对象
-   浏览器地址栏信息改变

时机：

-   如果请求中有表单数据，而数据又比较中重要，不能重复提交，建议使用重定向
-   如果请求被Servlet接收后，又无法进行处理，建议使用重定向定位到可以处理的资源