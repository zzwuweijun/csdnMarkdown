## Servlet（jsp）中文乱码

#### 请求编码格式

服务器得到浏览器发送回来的数据，但是浏览器一般是以ISO8859-1的编码格式去编码数据，而我们的服务器一般是以utf8的编码格式去编码数据，所以得到的数据是一堆编码。若想在服务器的到的是没有的乱码的中文，有下面几种方法：

-   万能方式：

    直接在获取浏览器传过来的数据后，再转码一次：

    `String = new String("浏览器传过来的用户数据".getBytes("iso8859-1"),"utf-8")`

    但是上面的方式处理少量的数据还可以，如果有很多数据要转码，就显的很繁琐。

-   Post请求方式：

    若浏览器的请求方式为post，则先设置如下代码，再获取用户数据：

    `rep.setCharacterEncoding("utf-8")`

    该代码的意思是服务器根据指定的编码格式重新编码浏览器传过来的用户数据。

    该方法要在获取用户数据之前设置，不然没有起作用。

-   Get请求方式：

    在Post请求方式的基础上，在tomcat的目录下的conf目录中修改servere.xml文件：在Connector标签中增加属性 `useBodyEncodingForURI=true`。

    ![1575424158895](Servlet%EF%BC%88jsp%EF%BC%89%E4%B8%AD%E6%96%87%E4%B9%B1%E7%A0%81.assets/1575424158895.png)





####　响应编码格式

服务器响应浏览器的请求并返回数据，同时还告诉浏览器以何种方式去解析返回的数据.

设置方法：

在响应对象(ServletRespone)中设置如下代码：

resp.setContentType("text/html;charset=utf-8");

或者使用下面等价代码：

resp.setHeader("Content-Type","text/html;charset=utf-8");



#### 有关链接

https://blog.csdn.net/Angelia620/article/details/86522898



https://www.iteye.com/blog/bijian1013-1765253



#### Servlet流程总结

-   浏览器发起请求到服务器
-   服务器接受浏览器的请求，进行解析，创建request对像存储请求数据
-   服务器调用对应的Servlet进行请求处理，并将request对象作为实参传递给Servlet的处理方法
-   Servlet的处理方法执行进行请求处理
    -   设置请求编码格式
    -   设置响应编码格式
    -   获取请求信息
    -   处理请求信息
        -   创建爱你业务层对象
        -   调用业务层对象的方法
    -   响应处理结果

