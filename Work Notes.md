# Work Notes

## 2019年12月16日

**1 返回高精度的系统时间（纳秒）**

```java
System.nanoTime();
```

**2 hutool工具类的使用**
 官网：
 https://www.hutool.cn/

 Maven:在项目的pom.xml的dependencies中加入以下内容:		

```xml
					
<dependency>
    <groupId>cn.hutool</groupId>
    <artifactId>hutool-all</artifactId>
    <version>5.0.7</version>
</dependency>
```

```java
//car-logic项目对该工具的使用：
//EquDataReportListener.java

String gpsTimeUtc = dataMap.get("gpsTime");
Date gpsDate = cn.hutool.core.DateUtil.parse(gpsTimeUtc);
//偏移后的
DateTime gpsDateTime = cn.hutool.core.date.DateUtil.offsetHour(gpsDate, 8);
```

**3 car-logic中EquDataReportListener.java中处理低功耗4种告警方法handleAlarm()中，在最后将StringBuilder转为字符串时，没有去掉最后一个逗号；**

**4 Strings工具类的使用**

```java
com.google.common.base.Strings;

String tripId = lastStatus.getOrDefault("tripId","");
Strings.isNullOrEmpty(tripId);
```

## 2019年12月17日

1 总结car-device项目中的消息体，将平台已实现的消息体进行分类，首先区分不同的协议，在各个协议中又分为可扩展和不可扩展两类，分类进行总结；

![消息体总结](images\平台已实现的消息体.png)

## 2019年12月18日

**1 复习昨天消息体总结；**

**2 更新了HttpResult代码，并在Controller层使用；**

**3 在项目中加入了PageHelper插件，对返回结果进行分页；**

**4 学习DecimalFormat类；**

   new DecimalFormat("0.##");

   new DecimalFormat("0.00");

#与0的区别：

 #：没有则为空；

 0：没有则补0；

**5 car-service-hw工程lbs下controller层代码**

**6 将消息体总结上传到Software-3；**

**7 结合car-device阅读netty官网用户手册部分内容；**

https://netty.io/wiki/user-guide-for-4.x.html

## 2019年12月19日

**1 编写基于netty的丢弃服务（DiscardServer）,并使用NetAssist工具调试成功，控制台打印输出hello netty;**

​       **Discard协议，抛弃协议**

　　它的作用就是接收到什么抛弃什么，它对调试网络状态的一定的用处。基于TCP的抛弃服务，如果服务器实现了抛弃协议，服务器就会在TCP端口9检测抛弃协议请求，在建立连接后并检测到请求后，就直接把接收到的数据直接抛弃，直到用户中断连接。而基于UDP协议的抛弃服务和基于TCP差不多，检测的端口是UDP端口9，功能也一样。  

​    在写代码的过程中，学习了捕获异常、添加if/while/try语句、选中行等快捷键；

**2 编写Echo Server**

​         **ECHO协议**：指的是把接收到的信息按照原样返回；作用：主要用于检测和调试；这个协议可以基于TCP/UDP协议用于服务器检测端口7有无信息。

**3 编写TIME Server**

**3.1 时间协议**

​        **时间协议**（英语：**TIME protocol**）是一个在[RFC](https://baike.baidu.com/item/RFC)868内定义的[网络传输协议](https://baike.baidu.com/item/网络传输协议)。它用作提供机器可读的日期时间信息。

​         时间协议可以在[TCP](https://baike.baidu.com/item/TCP)或[UDP](https://baike.baidu.com/item/UDP)上使用。在TCP上，主机会连接支持时间协议的服务器的TCP[端口](https://baike.baidu.com/item/端口)37。服务器会发送32位二进制数字然后断开连接，数字表示由[格林尼治标准时间](https://baike.baidu.com/item/格林尼治标准时间)1900年1月1日午夜0时0分0秒至当时的总秒数。主机在接收到时间后断开连接。

​        在UDP上，客户端会传送一个（通常为空的）数据包到UDP端口 37。服务器会把包含时间的数据包传回。在传送过程中没有进行连线。

​        现在，时间协议已经被网上时间协议（Network Time Protocol，NTP）所取代。

**3.2  2208988800**

*2208988800**为**1900**年**1**月**1**日**00:00:00~1970**年**1**月**1**日**00:00:00**的总秒数*

**3.3  Netty的用户使用手册已阅读完毕**

**4 开启办公机telnet功能；**

**5 学习尚硅谷Netty教程1-6节；**

**2019年12月20日**

**1 编写BIO编程服务端demo;**

​     手动创建线程池的问题；

​     String导错包导致响应的构造函数不可用；

​     telnet命令的使用: telnet 127.0.0.1 8888   ->  ctr+]

**2 学习Netty教程7-26节；**

