---
title: Http快速开始
description: Http快速开始
---

本文档将演示了如何快速使用Http请求接入ShenYu网关。您可以直接在工程下找到本文档的[示例代码](https://github.com/apache/incubator-shenyu/tree/master/shenyu-examples/shenyu-examples-http)。

## 环境准备

请参考[配置网关环境](../shenyu-set-up)并启动`shenyu-admin`。

引入网关对http的代理插件

* 在网关的 `pom.xml` 文件中增加如下依赖：

```xml
<!--if you use http proxy start this-->
<dependency>
    <groupId>org.apache.shenyu</groupId>
    <artifactId>shenyu-spring-boot-starter-plugin-divide</artifactId>
    <version>${last.version}</version>
</dependency>

<dependency>
    <groupId>org.apache.shenyu</groupId>
    <artifactId>shenyu-spring-boot-starter-plugin-httpclient</artifactId>
    <version>${last.version}</version>
</dependency>
```

启动`shenyu-bootstrap`项目。

## 运行shenyu-examples-http项目

下载[shenyu-examples-http](https://github.com/apache/incubator-shenyu/tree/master/shenyu-examples/shenyu-examples-http)

运行`org.dromara.shenyu.examples.http.ShenyuTestHttpApplication`main方法启动项目。

成功启动会有如下日志：
```shell
2021-02-10 00:57:07.561  INFO 3700 --- [pool-1-thread-1] o.d.s.client.common.utils.RegisterUtils  : http client register success: {"appName":"http","context":"/http","path":"/http/test/**","pathDesc":"","rpcType":"http","host":"192.168.50.13","port":8188,"ruleName":"/http/test/**","enabled":true,"registerMetaData":false} 
2021-02-10 00:57:07.577  INFO 3700 --- [pool-1-thread-1] o.d.s.client.common.utils.RegisterUtils  : http client register success: {"appName":"http","context":"/http","path":"/http/order/save","pathDesc":"Save order","rpcType":"http","host":"192.168.50.13","port":8188,"ruleName":"/http/order/save","enabled":true,"registerMetaData":false} 
2021-02-10 00:57:07.587  INFO 3700 --- [pool-1-thread-1] o.d.s.client.common.utils.RegisterUtils  : http client register success: {"appName":"http","context":"/http","path":"/http/order/path/**/name","pathDesc":"","rpcType":"http","host":"192.168.50.13","port":8188,"ruleName":"/http/order/path/**/name","enabled":true,"registerMetaData":false} 
2021-02-10 00:57:07.596  INFO 3700 --- [pool-1-thread-1] o.d.s.client.common.utils.RegisterUtils  : http client register success: {"appName":"http","context":"/http","path":"/http/order/findById","pathDesc":"Find by id","rpcType":"http","host":"192.168.50.13","port":8188,"ruleName":"/http/order/findById","enabled":true,"registerMetaData":false} 
2021-02-10 00:57:07.606  INFO 3700 --- [pool-1-thread-1] o.d.s.client.common.utils.RegisterUtils  : http client register success: {"appName":"http","context":"/http","path":"/http/order/path/**","pathDesc":"","rpcType":"http","host":"192.168.50.13","port":8188,"ruleName":"/http/order/path/**","enabled":true,"registerMetaData":false} 
2021-02-10 00:57:08.023  INFO 3700 --- [           main] o.s.b.web.embedded.netty.NettyWebServer  : Netty started on port(s): 8188
2021-02-10 00:57:08.026  INFO 3700 --- [           main] o.d.s.e.http.ShenyuTestHttpApplication     : Started ShenyuTestHttpApplication in 2.555 seconds (JVM running for 3.411) 
```

## 开启divide 插件来处理http请求

* 在 `shenyu-admin` 插件管理中，把`divide` 插件设置为开启。

## 测试Http请求
`shenyu-examples-http`项目成功启动之后会自动把加 `@ShenyuSpringMvcClient` 注解的接口方法注册到网关。

打开插件管理->divide 可以看到插件规则配置列表

![](/img/shenyu/quick-start/http/rule-list.png)

下面使用postman模拟http的方式来请求你的http服务

![](/img/shenyu/quick-start/http/postman-test.png)

