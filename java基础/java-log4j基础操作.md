## jdbc-jdbc基础操作

### 介绍

![1575813708693](java-log4j%E5%AD%A6%E4%B9%A0.assets/1575813708693.png)![1575813907643](java-log4j%E5%AD%A6%E4%B9%A0.assets/1575813907643.png)![1575819944268](java-log4j%E5%AD%A6%E4%B9%A0.assets/1575819944268.png)![1575819477833](java-log4j%E5%AD%A6%E4%B9%A0.assets/1575819477833.png)![1575819986786](java-log4j%E5%AD%A6%E4%B9%A0.assets/1575819986786.png)![1575820369879](java-log4j%E5%AD%A6%E4%B9%A0.assets/1575820369879.png)![1575820394271](java-log4j%E5%AD%A6%E4%B9%A0.assets/1575820394271.png)![1575820479822](java-log4j%E5%AD%A6%E4%B9%A0.assets/1575820479822.png)![1575820602795](java-log4j%E5%AD%A6%E4%B9%A0.assets/1575820602795.png)

### 常用类

-   org.apache.log4j.ConsoleAppender
-   org.apache.log4j.DailyRollingFileAppender
-   org.apache.log4j.RollingFileAppender
-   org.apache.log4j.PatternLayout

### 使用log4j

org.apache.log4j.Logger log =org.apache.log4j.Logger.getLogger(test.class); 

log.all(Object message);

log.debug(Object message);

log.info(Object message);

log.warn(Object message);

log.error(Object message);



### 输出文件路径

log4j.appender.AppendersName.filr = 绝对路径（相对磁盘）和相对路径（相对项目根目录）



### 设置追加

log4j.appender.AppendersName.Append = true

### 设置级别

log4j.appender.AppendersName.Threshold = ERROR 

大于或等于设置的级别才能进行相应的操作

