# MQ 事务消息纳入全局事务管理样例

本样例介绍如何把 MQ 事务消息的发送纳入 GTS 管理的全局事务。

在把 MQ 事务消息的发送纳入 GTS 管理的全局事务，请先完成以下工作：

-   准备一个可用的 MySQL 环境（可以是阿里云的 RDS）。
-   准备一个可用的 Maven 环境。

## 样例说明

样例工程模拟了资金转账的应用。包含 2 个数据源，和 1 个 MQ 事务消息 Topic：

-   帐户 A 数据源：存储 A 的资金。
-   帐户 B 数据源：存储 B 的资金。
-   MQ 事务消息 Topic：衔接上下游业务的消息队列。

## 步骤一：下载样例工程

样例工程请参见 [gts-sample-mq](https://code.aliyun.com/txc-console/gts-sample-mq/repository/archive.zip?ref=master)。

## 步骤二：构建样例工程

1.  初始化数据库。

    1.  创建两个用于运行样例的数据库。

    2.  分别执行工程中的 init-a.sql 和 init-b.sql 脚本，建立相关表。

2.  在样例工程的根目录下，执行 `mvn clean install`命令，构建样例工程。

    运行成功后`common/lib`目录下会生成 GTS 的 SDK 包，包括：

    -   客户端主包：~txc-client-$\{gts.sdk.version\}.jar
    -   Spring Cloud 原生支持包：txc-client-springcloud-$\{gts.sdk.version\}.jar

## 步骤三：导入样例工程到 IDE

为了方便运行和理解，建议您把工程导入到 IDE 中。

## 步骤四：运行样例工程

运行样例工程中 Application 的 Main 方法，结合代码逻辑，查看 console 的日志输出。

## 关键配置和运行机制解读

`application.properties`中，以 spring.cloud.txc 为前缀的一系列参数是 GTS 关键配置，说明如下：

-   GTS 全局事务调用链路上的每个服务都要进行这些配置，例如样例中的 Business/Storage/Order/Account。
-   spring.cloud.txc.txcAppName：每个服务自定义一个全局唯一的应用名。
-   spring.cloud.txc.txcServerGroup：GTS 服务实例（事务分组）名。
    -   在本地运行通过公网访问 GTS 服务时，请使用公共的实例 txc\_test\_public.1129\*\*\*\*3855\*\*\*\*.QD 并配合使用下面的 spring.cloud.txc.url 配置。
    -   在正式环境 ECS 上运行时，请使用您订购的 GTS 服务实例全名，并配合使用下面的 spring.cloud.txc.accessKey 和 spring.cloud.txc.accessKey 配置。
-   spring.cloud.txc.mode： GTS 工作模式，默认为 1（AT 模式）。MQ 实际上使用了 TCC 模式，所以这里模式为 3。
-   spring.cloud.txc.url：公网访问 GTS 服务的接入地址，固定值 `https://test-cs-gts.aliyuncs.com` 。这个配置仅在本地公网访问时需要。
-   spring.cloud.txc.accessKey和`spring.cloud.txc.secretKey`：在 ECS 上正式运行，这里配置您 GTS 服务实例使用者的 AK 和 SK 用于鉴权。默认是使用订购 GTS 服务实例的用户（即实例全名中间部分 **账号ID** 对应用户）的 AK 和 SK。也可以使用 RAM 授权的用户 AK 和 SK，具体方法请参见[为 RAM 用户授权事务分组](/cn.zh-CN/最佳实践/为 RAM 用户授权事务分组.md)。

