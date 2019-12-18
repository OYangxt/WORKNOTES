# Work Notes

## 2019年12月15日

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

## 2019年12月16日

1 总结car-device项目中的消息体，将平台已实现的消息体进行分类，首先区分不同的协议，在各个协议中又分为可扩展和不可扩展两类，分类进行总结；

![消息体总结](images\平台已实现的消息体.png)