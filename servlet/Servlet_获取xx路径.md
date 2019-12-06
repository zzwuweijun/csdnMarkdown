## Servlet中获取绝对路径的常见方法

通过ServletContext的getRealPath()方法

```java
//获得ServletContext对象
ServletContext servletContext = this.getServletContext();
//获得资源的绝对路径
String path = servletContext.getRealPath("...");
```

注意：括号中传入的路径为该资源相对于该项目的路径

---

