## jdbc 的PrepareStatement 中文参数 ？问题

今天遇到一个有关jdbc链接数据库的问题，就是使用PreparedStatement类的占位符进行条件搜索，一加上中文，就给报 什么--中文参数全部变成了？（问号）-- 这样的错误，搞得我好烦，但是在Navicat里面运行sql语句就能够执行，真是奇了怪了，这说明sql语句没有错误了啊，又看了下逻辑代码，也是没有问题的，因为如果占位符输入的不是中文的话，又能成功执行，能查询到数据，一有中文就报错，好了，问题到这里就很明确了，可以判断是编码问题了。。。

下面来解决数据库的编码问题：

 一、将MYSQL编码设置为 `utf8_unicode_ci`

  二、将连接字符串设置成`jdbc:mysql://localhost:3306/my_servletjsptest?useUnicode=true&characterEncoding=UTF-8`

完成面操作就能完美执行了。

。。。

在创建数据库的时候，选择编码格式为：

字符集：`utf8 -- UTF-8 Unicode`

排序规则：`utf8_unicode_ci`



