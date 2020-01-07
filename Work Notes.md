# Work Notes

# 第1周

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

## 2019年12月20日

**1 编写BIO编程服务端demo;**

​     手动创建线程池的问题；

​     String导错包导致响应的构造函数不可用；

​     telnet命令的使用: telnet 127.0.0.1 8888   ->  ctr+]

**2 学习Netty教程7-26节；**

## 2019年12月21日

**1 准备DE类人才认定材料；**

**2 学习car-service项目下，app模块；**

**3 学习car-service项目下，bizmgr模块；**

* Object userObJ = SecurityUtils.getSubject().getPrincipal();

​        在shiro中，如果正常登陆（执行subject.login(token)成功），就能在全局通过SecurityUtils.getSubject().getPrincipal();获取用户信息。

* BeanUtils.copyProperties(userObj, user);

# 第2周

## **2019年12月23日**

**1 提交党员转正材料给支部书记；**

**2 写NIOServer和NIOClient代码；**

**3 阅读car-service工程下sysmgr模块代码；**

**4 提交DE类人才认定材料；**

**5 向王帆询问薛博文所提的问题（在告警结束前平台不能保存告警信息），**阅读logic代码可知，

​       平台不会重复保存同一类型的告警信息，所以在同一个告警信息为结束前，不会保存期间上报的同一类型的数据，但不影响GPS位置信息的上报；

**6 学习尚硅谷netty视频教程27-32节，写群聊代码；**

## 2019年12月24日

**1 复习mybatis相关知识；**

   两种实现方式（写dao接口实现类，不写实现类），与spring的集成，拦截器

**2 复习Redis相关知识；**

**3 复习RabbitMq知识；五种队列和消息分发模式；**

**4 JIRA转移责任人：点备注,添加信息，该责任人即可；**

**5 学习Reactor模式:**

​    单线程单Reactor，单Reactor多线程，主从Reactor；

**6 学习Netty模型**

 BossGroup，WorkGroup，NioEventLoopGroup

accept事件，NioSocketChannel，PipeLine，handler

**7 NIO与零拷贝**

**8 学习Netty视频教程33-43**

## 2019年12月25日

**1 复习昨天所学知识，主要是netty相关；**

**2 mybatis中resultType总结**

resultType:

​	基本类型 ：resultType=基本类型

​	List类型：   resultType=List中元素的类型

​	Map类型：  单条记录：resultType =map
​                      多条记录：resultType =Map中value的类型

**3 在微服务中添加Redis缓存**

​        实现部门信息查询时，先根据key从Redis中查找，如果不存在，从数据库中查找，再存入Redis中。

**4 使用TortoiseGit提交代码，比较与上一版本的差异；**

**5 参加党支部大会；**

**6 学习netty教程44-46；**

netty服务端和客户端编程；

## 2019年12月26日

**学习接入云项目代码：**

iotcloud-device相关；

## 2019年12月27日

**1 写转正PPT；**

**2 师傅带着过了一下device工程代码的流程**

**3 复习Feign的使用；**

**4 学了一个idea快捷键，shift+ctrl+上下方向键，上下移动；**

**5 连接接入云11上的数据库，查看Eureka下的所有微服务；**

**6 查看接入云项目相关的api文档；**

**7 复习Hystrix和Zuul；**

## 2019年12月28日

做转正PPT

# 第3周

## 2019年12月30日

**1 整理接入云项目结构；**

**2 查看device-service工程代码提交历史；**

**3 查看product微服务的接口和配置文件；**

**4 HttpServletRequest类通过getInputStream()方法来获取body；**

**5 学习原码，反码和补码；**

   正数的原码、反码和补码都相同；

  负数的原码为：将其绝对值的原码的首位置1，

  负数的反码为：将其原码除符号位外取反，

  负数的补码为：将其反码+1

**6 测试ByteBuf类中readUnsignShort()方法和readShort()方法的不同；**

**7 @PathVariable注解标识的参数，会拼接到URL中，此处无需判断参数传递；**

**8 了解HTTP协议的长连接和短连接；**

**9 修改微服务中Redis的使用，加入RedisDao及其实现类；**

## 2019年12月31日

**1 回忆昨天所学内容；**

**2 更新接入云代码；**

**3 使用Junit测试FastJson；**

​    将实体类转为JSON字符串；

​    将JSON字符串转为实体类；

​    将JSON字符串转为Map对象，并根据键获取值；

**4 @AllArgsConstrustor属于lombok**

@Data
使用这个注解，就不用再去手写Getter,Setter,equals,canEqual,hasCode,toString等方法了，注解后在编译时会自动加进去。
@AllArgsConstructor
使用后添加一个构造函数，该构造函数含有所有已声明字段属性参数
@NoArgsConstructor
使用后创建一个无参构造函数
**5 查看oc适配器代码；**

**6 查看产品微服务代码；**

# 2020年1月1日

# HAPPY NEW YEAR !

## 2020年1月2日

**1 更换桌面背景；**

**2 修改转正PPT;**

**3 复习Spring；**

* IOC(Inversion of Control)控制反转

  * 首先，从对象创建方式的改变进行理解：

    由程序员手动new对象，到只需要声明一个接口，而不需要new实现类，降低了业务层对持久层的依赖；

  * 其次，new对象时，其实需要一些创建对象的资源，现将这种获取资源的主动权利，由程序员转交到框架手里，交给框架去控制资源，则为控制反转；

* 基于xml配置文件的IOC

  * 实例化bean的三种方式
    * 默认使用无参构造函数
    * 通过Spring管理静态工厂类
    * 通过Spring管理实例化工厂类
  * 依赖注入的三种方式
    * 构造函数
    * set方法
    * p名称空间

* 基于注解的IOC

  * 注入bean的
    * @Component
    * @Controller
    * @Service
    * @Repository
  * 数据相关的
    * @Autowire
    * @Qualifier必须与@Autowire连用
    * @Resource

**4 复习SpringMVC阅读第一天笔记；**

**5 学习Netty教程；**

## 2020年1月3日

**1 复习SpringMVC的响应数据和结果视图，异常处理和拦截器；**

**2 复习SSM框架的整合；**

**3 学习消息总线基础；**

**4 回顾car-device已实现消息体，并修改对应的总结文档；**

**5 安装虚拟机；**

**6 定位测试部发来的问题；**

## 2020年1月4日

主要工作修改透传信息代码；

# 第4周

## 2020年1月6日

1 学习T101协议和代码，并与导师沟通；

2 提交转正PPT;

3 提交透传信息优化代码；

## 2020年1月7日

1 写定时任务代码；

2 转正答辩；

3 阅读接入云和管道云项目框架；

4 学习netty异步模型原理和任务队列（taskQueue）； 

