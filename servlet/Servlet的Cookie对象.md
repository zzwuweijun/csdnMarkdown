## Servlet的Cookie对象

作用：解决了发送的不同请求的数据共享问题

---

使用：

### Cookie的创建和存储

#### 创建Cookie对象

`Cookie c = new Cookie(String name, String value)`

#### 设置Cookie(有多种设置)

-   设置有效期

    `c.setMaxAge(int seconds)`

    设置该Cookie在浏览器中保留的秒数

    

-   设置有效路径

    `c.setPath(String uri)`

    有效路径设置后，只用该路径才能够访问到该Cookie，其他路径访问不到。

#### 响应Cookie信息给浏览器客户端

`resp.addCookie(c)`



### Cookie的获取

-   获取Cookie信息数组

    `Cookie[] ck= req.getCookies()`

-   遍历数组获取Cookie信息

    ```java
    if(c != null){
        for(Cookie c : ck){
            String name = c.getName();
            String value = c.getValue();
        }
    }
    ```

---

注意：

一个Cookie对象存储一条数据。多条数据，可以创建多个Cookie对象进行存储。

---

特点：

浏览器端的数据存储技术

存储的数据声明在服务器端

临时存储：存储在浏览器的运行内存中，浏览器光比及失效

定时存储：设置Cookie的有效期，存储在浏览器的磁盘中，在有效期内并符合有效路径的请求都会附带该信息

默认Coolkie信息存储好之后，每次请求都会附带，除非设置有效路径

---

