## web.xml文件的作用

### web.xml文件的作用

 每个javaEE工程中都有web.xml文件，那么它的作用是什么呢？它是每个web.xml工程都必须的吗？  

 一个web中可以没有web.xml文件，也就是说，web.xml文件并不是web工程必须的。web.xml并不是一个Web的必要文件，没有web.xml，网站仍然是可以正常工作的。只不过网站的功能复杂起来后，web.xml的确有非常大用处，所以，默认创建的动态web工程在WEB-INF文件夹下面都有一个web.xml文件。 

 web.xml文件是用来初始化配置信息：比如Welcome页面、servlet、servlet-mapping、filter、listener、启动加载级别等。当你的web工程没用到这些时，你可以不用web.xml文件来配置你的Application。 

 每个xml文件都有定义它书写规则的Schema文件，也就是说javaEE的定义web.xml所对应的xml  Schema文件中定义了多少种标签元素，web.xml中就可以出现它所定义的标签元素，也就具备哪些特定的功能。web.xml的模式文件是由Sun 公司定义的，每个web.xml文件的根元素为<web-app>中，必须标明这个web.xml使用的是哪个模式文件。如：

```xml
<?xml version="1.0" encoding="UTF-8"?> 
<web-app version="2.5" 
xmlns="http://java.sun.com/xml/ns/javaee" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xsi:schemaLocation="http://java.sun.com/xml/ns/javaee 
http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"> 
    其他的功能标签写在这里。。。。，例如：
    <welcone-file-list>...</welcone-file-list>
    ...
</web-app> 
```

 上面说了web.xml文件的作用，下面就说该文件中的具体设置，也就是各个功能模块要怎么去设置。

### 设置欢迎页面

每次打开一个应用程序，都应该自动的为用户启动一个默认的欢迎页面（嗯，首页了解一下）。实现方法如下：

```xml
<welcome-file-list> 
    <welcome-file>index.jsp</welcome-file> 
    <welcome-file>index.html</welcome-file> 
    ...
</welcome-file-list> 
```

 指定了2个欢迎页面，显示时按顺序从第一个找起，如果第一个存在，就显示第一个，后面的不起作用。如果第一个不存在，就找第二个，以此类推。 



### 设置Servlet

每一应用程序可以有许多的Servlet，而且设置Servlet的方式有多种，目前博主知道的方式就有两中，一种是通过注解（WebServlet）设置Servlet，另一种就是通过该web.xml文件来设置了。在此只讲如何通过web.xml文件的形式来设置Servlet，注解方式自行搜索。

为什么不讲注解方式么？主要是注解方式设置的Servlet，一旦编译过后，就不能再修改了，除非再次编译；而通过该web.xml文件设置的Servlet可以在编译后随便更改，并不用在此编译。

下面讲如何实现：

设置Servlet要用到两个标签这两个标签是绑定在一起的，只用其一是不起作用的，一个是为Servlet命名，一个是为Servlet定制URL。代码走起。。。

```xml
<servlet> 
    <servlet-name>servlet1</servlet-name> 
    <servlet-class>org.whatisjava.TestServlet</servlet-class> 
</servlet> 
<servlet-mapping> 
    <servlet-name>servlet1</servlet-name> 
    <url-pattern>*.do</url-pattern> 
</servlet-mapping>
```

可以看了代码后一脸懵逼，没关系，现在来说下各个标签的作用。

首先是 `<servlet>` 标签，该标签的作用主要有为Servlet命名、链接到某个java类、启动级别等。

相信看过代码的你不难发现 `<servlet-name>` 出现过两次，这时为什么呢，解决问题之前先说下`<servlet-name>` 标签的作用，没错，很容易就看出是为Servlet命名；那再来说说为什么会出现两次，在上文中博主已经说过，一个应用程序中可以有许多的Servlet，并且每一个Servlet都是有两个标签组合而成，可想而知，想要知道一个Servlet是有哪两个标签，就要有一个中间变量来寻找这两个标签，而`<servlet-name>` 这个标签就是充当这个中间变量了。

在来说说 `<servlet-class>` 标签的作用，我么知道一个Servlet的调用，实际上就是调用一个java类。那么我们是怎么告诉机器去调用那个java类的呢？这就是该标签的作用了。ps：按住ctrl键并鼠标一到该类名上，类名颜色改变，并点击能跳转到该java类，则是类名设置正确无误。

下面说说 `<servlet-mapping>` 标签的作用，该标签中只用两个子标签，`<servlet-name>` 和 `<url-pattern>` 。`<servlet-mapping>` 标签主要是实现一种映射关系，即是访问特定的URL（URL模式），就能够调用 `<servlet-class>` 标签绑定的java类。那么是怎么设置URL模式的呢，是在 `<url-pattern>` 标签中设置的，如果 `<url-pattern>` 定义的是路径，那么以后所有对这个路径下资源的请求都会由`<servlet-name>`中定义的servlet处理；如果`<url-pattern>`定义的是资源格式例如*.do等，那么对于所有符合这种格式的资源的请求都由指定的servlet处理。 

===============

实例：

现有一个名为 myServlet1的项目，项目中有一个java类：MyServlet.java，代码：

```java
public class MyServlet extends HttpServlet {
	@Override
	protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		resp.getWriter().write("heollo,worl");
		System.out.print("hello wirl...");
		
	}

}
```

现设置一个新的Servlet，URL模式为 `/first` ,代码：

```xml
<servlet> 
    <servlet-name>servlet01</servlet-name> 
    <servlet-class>com.wwj.servlet.myServlet1</servlet-class> 
</servlet> 
<servlet-mapping> 
    <servlet-name>servlet01</servlet-name> 
    <url-pattern>/my</url-pattern> 
</servlet-mapping>
```

在浏览器地址栏中输入：http://localhost:8080/myServlet1/my，即可在页面中打印"hello wirl..."：

![https://raw.githubusercontent.com/zzwuweijun/csdnMarkdown/master/servlet/web/1575126111141.png](https://raw.githubusercontent.com/zzwuweijun/csdnMarkdown/master/servlet/web/1575126111141.png)

====================

虽然通过上面就能够设置基本的Servlet，但是作为程序员的我们并不能满足于此。

`<servlet>` 标签除了上面的两个子标签外，还有一下子标签：

![1575196949602](web%E6%96%87%E4%BB%B6.assets/1575196949602.png)

下面就单独讲解部分标签的作用：

`<load-on-startup>`： 标记容器是否在启动的时候就加载这个servlet。  当值为0或者大于0时，表示容器在应用启动时就加载这个servlet；  当是一个负数时或者没有指定时，则指示容器在该servlet被选择时才加载。  正数的值越小，启动该servlet的优先级越高。 如果我们在web.xml中设置了多个servlet的时候，可以使用load-on-startup来指定servlet的加载顺序，服务器会根据load-on-startup的大小依次对servlet进行初始化。不过即使我们将<load-on-startup>设置重复也不会出现异常，服务器会自己决定初始化顺序。

`<async-supported>`： 作用是支持异步处理。 

`<description>`： 用于描述servlet的相关信息 

`<display-name>`： servlet的描述性说明文字 

`<init-param>`：用于设置several的初始参数。一个Servlet可以有多个`<init-param>`标签。该标签有三个子标签，`<description></description>`、`<param-name></param-name>`、`<param-value></param-value>`，看名字都能看出是啥意思。。。	在java类中通过 `config.getInitParameter("param-value");`来获取。

`<jsp-file>`： 等同于<servlet-class>一样，只是现在是要用jsp来替代servlet的功能。本质上jsp就是servlet 

`<multipart-config>`：与上传文件有关。



### 设置error界面

先贴出代码：

```xml
	<error-page>
		<error-code>404</error-code>
		<location>/404.html</location>
	</error-page>

	<error-page>
		<error-code>405</error-code>
		<location>/WEB-INF/405.html</location>
	</error-page>
```

如果浏览器出现404、405错误，则会调用上面的界面，不会给客户返回一堆代码。。。


=======


