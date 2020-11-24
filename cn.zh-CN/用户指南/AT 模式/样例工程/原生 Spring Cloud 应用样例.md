# 原生 Spring Cloud 应用样例

GTS SDK 2.8.31 版本开始，GTS 全面支持原生 Spring Cloud 应用，包括 RestTemplate 和 Feign 两种方式。

在使用原生 Spring Cloud 应用样例前，请先完成以下工作：

-   数据库依赖 MySQL，准备一个可用的 MySQL 环境（也可以是阿里云的 RDS）。
-   构建样例工程依赖 Maven，准备一个可用的 Maven 环境。

## 样例简介

该样例模拟了一个用户订购商品的业务系统，包含 3 个微服务：

-   Storage：库存服务，扣减指定商品的库存数量。
-   Order：订单服务，根据采购请求生成订单。
-   Account：账户服务，从用户账户中扣减金额。

订购商品的业务流程如下图所示：

![样例场景-Spring Cloud](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1136998851/p89050.png)

1.  Business 开启一个 GTS 管理的全局事务。
2.  Business 调用 Storage 和 Order。
3.  Order 调用 Account。

GTS 将保障整个服务调用链路上的数据一致性。

## 步骤一：下载样例工程

样例工程详情请参见 [Spring Cloud 原生支持样例源代码](https://code.aliyun.com/txc-console/gts-sample-springcloud/repository/archive.zip?ref=master)。

## 步骤二：构建样例工程

1.  创建一个用于运行样例的数据库，执行工程中的 `init.sql` 脚本，建立相关表。

2.  构建样例工程。

    1.  构建样例工程依赖 Maven，准备一个可用的 Maven 环境。

    2.  在样例工程的根目录下，执行`mvn clean install`命令。

    SDK 包是由common/lib里的`download-maven-plugin`插件通过wget命令从 GTS 官网下载的。如果您的环境不能执行wget命令，上面的 Maven 构建会失败。这种情况下，请您按以下方式操作：

    1.  手工下载最新的 [SDK 开发包](http://txc-console.oss-cn-beijing.aliyuncs.com/sdk/txc-client-2.9.0.jar?spm=a2c4g.11186623.2.10.747d359d5AvWYq&file=txc-client-2.9.0.jar)，并放在 common/lib 目录下。
    2.  在工程 pom.xml 文件的 `modules` 中将`common` 删掉。

        ```
        <modules>
         <!--<module>common</module>-->
         <module>bussiness</module>
         <module>account</module>
         <module>storage</module>
         <module>order</module>
         <module>eureka</module>
        </modules>                            
        ```

    3.  重新执行 `mvn clean install` 命令。
    运行成功后`common/lib`目录下会生成 GTS 的 SDK 包，包括：

    -   客户端主包：~txc-client-$\{gts.sdk.version\}.jar
    -   Spring Cloud 原生支持包：txc-client-springcloud-$\{gts.sdk.version\}.jar

## 步骤三：导入样例工程到 IDE

为了方便运行和理解，建议您把工程导入到 IDE 中。

## 步骤四：运行样例工程

1.  分别运行样例工程中 5 个 module 的 Main 方法，启动服务。

    -   Eureke：EurekaServerApplication
    -   Storage：StorageApplication
    -   Order：OrderApplication
    -   Account：AccountApplication
    -   Business：BusinessApplication
2.  服务启动成功后，通过浏览器访问 http://127.0.0.1:8084/purchase 来调用订购业务。

    **说明：** 可选的调用参数请阅读样例中的 BusinessController.java 的代码来了解。


## 关键配置和运行机制解读

`application.properties`中，`spring.cloud.txc` 前缀的一系列配置是 GTS 关键配置，说明如下：

-   GTS 全局事务调用链路上的每个服务都要做这些配置，例如样例中的 Business/Storage/Order/Account。
-   `spring.cloud.txc.txcAppName`：为每个服务定义一个全局唯一的名字。
-   `spring.cloud.txc.txcServerGroup`：GTS 服务实例名。

    -   在本地运行通过公网访问 GTS 服务时，请使用公共的实例 `txc_test_public.1129361738553704.QD` 并配合使用下面的 `spring.cloud.txc.url` 配置。
    -   在正式环境 ECS 上运行时，请使用您订购的 GTS 服务实例全名，并配合使用下面的 `spring.cloud.txc.accessKey` 和 `spring.cloud.txc.accessKey` 配置。
-   `spring.cloud.txc.url`：公网访问 GTS 服务的接入地址，固定值 `https://test-cs-gts.aliyuncs.com` 。这个配置仅在本地公网访问时需要。
-   `spring.cloud.txc.accessKey`和`spring.cloud.txc.secretKey`：在 ECS 上正式运行，这里配置您 GTS 服务实例使用者的 AK 和 SK 用于鉴权。默认是使用订购 GTS 服务实例的用户（即实例全名中间部分 **账号ID** 对应用户）的 AK 和 SK。也可以使用 RAM 授权的用户 AK 和 SK，具体方法请参见[为 RAM 用户授权事务分组](/cn.zh-CN/最佳实践/为 RAM 用户授权事务分组.md)。

