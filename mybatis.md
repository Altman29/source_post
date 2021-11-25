---
title: mybatis
date: 2021-11-25 14:58:03
tags: [mybatis]
categories: [mybatis]

---

## 主题

Mybatis基于XML和注解方式的开发应用专题

## 目标

- 主键返回

- 批量查询

- 动态传参

- 查询缓存(一级缓存、二级缓存)

- 延迟加载(侵入式延迟加载、深度延迟加载)

- 关联查询(一对一、一对多映射)

- 逆向工程

- PageHelper分页插件

- 注解开发



## 入门篇

### 编写流程

1.编写全局配置文件: SqlMapConfig.xml(数据库配置等)

2.映射文件: xxxMapper.xml(根据需求编写SQL语句)

3.编写dao代码: xxxDao接口、xxxDaoImpl实现类(编写mybatis API)

4.POJO类(用来传递参数和映射结果对象)

5.单元测试类

### phase01 findUserById

pom.xml:添加依赖

<img src="https://cdn.jsdelivr.net/gh/Altman29/cloudimg/bucket/202111251451573.png" style="zoom:50%;" />

resources:添加db.properties 来连接数据库

<img src="https://cdn.jsdelivr.net/gh/Altman29/cloudimg/bucket/202111251452272.png" style="zoom:50%;" />

SqlMapConfig.xml: 使用db.properties来配置连接(全局配置文件)（spring提供）&加入mapper(映射文件)

<img src="https://cdn.jsdelivr.net/gh/Altman29/cloudimg/bucket/202111251452707.png" style="zoom:50%;" />

UserMapper.xml: 按需求写sql mapper

<img src="https://cdn.jsdelivr.net/gh/Altman29/cloudimg/bucket/202111251452171.png" style="zoom:50%;" />

创建User表: 见db_local.phase01.users

<img src="https://cdn.jsdelivr.net/gh/Altman29/cloudimg/bucket/202111251453091.png" style="zoom:50%;" />

创建User POJO对象: User.class

<img src="https://cdn.jsdelivr.net/gh/Altman29/cloudimg/bucket/202111251453129.png" style="zoom:50%;" />

UserDao&UserDaoImpl: 具体实现

<img src="https://cdn.jsdelivr.net/gh/Altman29/cloudimg/bucket/202111251453847.png" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Altman29/cloudimg/bucket/202111251453202.png" style="zoom:50%;" />

Test: 测试

<img src="https://cdn.jsdelivr.net/gh/Altman29/cloudimg/bucket/202111251454721.png" style="zoom:50%;" />



success:

<img src="https://cdn.jsdelivr.net/gh/Altman29/cloudimg/bucket/202111251526478.png" style="zoom:50%;" />

[Talk is cheap. Show me the code(传送门)](https://github.com/Altman29/JavaTraining)

---



#### 遇到问题

__`PersistenceException`异常产生和处理__

>org.apache.ibatis.exceptions.PersistenceException: 
>
>Error building SqlSession.
>
>The error may exist in SQL Mapper Configuration
>
>Cause: org.apache.ibatis.builder.BuilderException: Error parsing SQL Mapper Configuration. Cause: java.io.IOException: Could not find resource db.properties

_解决：SqlMapConfig.xml中<properites>中设置正确路径；_

__`PersistenceException` +1__

> org.apache.ibatis.exceptions.PersistenceException: 
>
> Error building SqlSession.
>
> The error may exist in UserMapper.xml
>
> Cause: org.apache.ibatis.builder.BuilderException: Error parsing SQL Mapper Configuration. Cause: java.io.IOException: Could not find resource UserMapper.xml

_解决：SqlMapConfig.xml中<mappers>中设置正确路径；_

__`WARN`__

> Thu Nov 25 14:09:13 CST 2021 WARN: Establishing SSL connection without server's identity verification is not recommended. According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be established by default if explicit option isn't set. For compliance with existing applications not using SSL the verifyServerCertificate property is set to 'false'. You need either to explicitly disable SSL by setting useSSL=false, or set useSSL=true and provide truststore for server certificate verification.

翻译：

>不建议在没有服务器身份验证的情况下建立SSL连接,根据MySQL 5.5.45+、5.6.26+和5.7.6+的要求，如果没有设置显式选项，则必须默认建立SSL连接。为了符合不使用SSL的现有应用程序，verifyServerCertificate属性被设置为“false”。您需要通过设置useSSL=false显式禁用SSL，或者设置useSSL=true并为服务器证书验证提供信任存储。

_解决:_

不建议在没有服务器身份验证的情况下建立SSL连接,只是不建议,如果你执意这么做的话呢,当然可以无视,那么如果你接受了人家的建议,该怎么解决这个问题呢?很简单,在你连接数据库的url后面加上参数即可，例如:

` jdbc:mysql://localhost:3306/testdb?useSSL=false`即可，不再显示WARN。



至此，一个简单的mybatis入门使用示例完成。



