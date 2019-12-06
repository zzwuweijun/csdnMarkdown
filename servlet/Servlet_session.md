## session 使用

问题：

-   一个用户的不同请求处理的数据共享怎么办？
-   前面有学到的Cookie能够解决上述问题，但是这样多个用户之间的请求都能共享一个相同的Cookie，这就照成数据安全问题。

---

解决：

-   使用session技术

---

原理：

-   用户第一次访问服务器，服务器会创建一个session对象给此用户，并将该session对象的JSESSIONID使用Cookie技术存储到浏览器中，保证用户的其他请求能够获取到同一个session对象，也保证了不同请求能够获取到共享的数据。

---

特点：

-   存储在服务器端
-   有服务器端创建
-   依赖Cookie技术
-   一次回话
-   默认存储时间30分钟

---

作用：

-   解决了一个用户不同请求处理的数据共享问题

---

使用：

-   创建session对象/获取色素sin对象

    -   `HttpSession hs = req.getSession();`
    -   如果请求中拥有session的标识符，也就是JSESSIONID，则返回其对应的session对象

    

    -   如果请求中没有session的标识符，则创建新的session对象，并将其JSESSIONID作为Cookie数据传给浏览器内存中。

    

    -   如果session对象失效了，也会重新创建一个session对象，并将其JSESSIONID存储在浏览器内存中。
    -   获取JSESSIONID的值：`hs.getID();`

    

-   设置session存储时间

    -   `hs.setMaxInactiveInterval(int seconds);`
    -   注意：在指定的时间内session对象没有被使用则销毁，如果使用了则重新计时。如果服务器重启了，浏览器保存的JSESSIONID一样会失效。

    

-   设置session强制失效

    -   `hs.invalidate();`
    -   一般用于退出登录



-   存储和获取数据
    -   存储：
        -   `hs.setAttribute(String name, Object value);`
    -   获取：
        -   `hs.getAttribute(String name);`
        -   返回的数据类型为Object
    -   注意：
        -   存储的动作和获取的动作发生在不同的请求中，但是存储要在先，后在获取。
-   使用时机
    -   一般用户在登录web及项目是会将用户的个人信息存储到session中，供该用户的其他请求服务。 
-   总结
    -   session解决了一个用户的不同请求的数据共享问题，只要在JSESSIONID不失效和Session对象不失效的情况下，永固的任意请求在处理是都能获取到同一个session对象。
-   作用域
    -   一次回话
    -   在JSESSIONID和Session对象不失效的情况下为整个项目提供支持。
-   session失效处理
    -   将用户请求中的JSESSIONID和后台获取到的Session对象的JSESSIONID进行比较，一致则不失效，不一致则失效。重定向到登录界面。

---

注意：

-   JSESSIONID存储在了Cookie的临时存储空间中，浏览器关闭即失效。
-   