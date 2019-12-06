## Servlet的ServletContext对象使用

问题：

-   Request解决了一次请求内的数据共享问题；Session解决了用户不同请求的数据共享问题，Cookie解决了也是用户不同请求的数据共享问题，但没有Session的安全级别高，那么不同的用户的数据共享该怎么解决？

---

解决：

-   使用ServletContext对象

---

作用：

-   解决了不同用户的数据共享问题

---

原理：

-   ServletContext对象有服务器进行创建，一个项目只有一个servletContextdx对象。不管在项目的任意位置进行获取得到的都是同一个对象，那么不同用户发起的请求获取到的也就是同一个对象了，该对象由用户共同拥有。
-   一个项目只有一个

---

特点：

-   由服务器创建

---

使用：

-   获取servletContext对象,有三中方式

    -   `ServletContext sc = this.getSrvletContext();`
    -   `ServletContext sc = this.getServletConfig().getServletContext();`
    -   `ServletContext sc = req.getServletContext();`

    

-   使用servletContext对象完成数据共享

    -   设置ServletContext对象

        -   `sc.setAttribute(String name, Object o);`

        

    -   获取ServletContext对象的数据

        -   `sc.getAttribute(name);`

        

    -   注意

        -   不同的用户可以给ServletContext对象进行数据的存取

        -   获取的数据不存在，返回Null

        

-   在web.xml文件中设置全局数据

    -   实现方式

        ```xml
        <context-param>
        	<param-name>name</param-name>
        	<param-value>全局数据</param-value>
        </context-param>
        ```

        有多个数据，就写多个 `<context-param>` 标签。在这里只能写String类型的数据。

        该标签和ServletContext对象相互对应，所有能够使用ServletContext对象来获取到该标签设置的值。

        

    -   获取全局数据

        要有ServletContext对象的实例，再用实例调用 `getInitParameter(String name);` 方法获取全局数据。

        

    -   作用

        -   使静态数据和代码解耦

---

