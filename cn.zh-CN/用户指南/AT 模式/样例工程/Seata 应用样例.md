# Seata 应用样例

Seata 是基于全局事务服务 GTS 的开源分布式事务解决方案，和 GTS 的核心原理和事务协议是完全一致的。本文通过样例介绍如何将一个基于 Seata 的分布式事务应用迁移到 GTS 上运行。

在使用Seata 应用样例前，请先完成以下工作：

-   数据库依赖 MySQL，准备一个可用的 MySQL 环境（也可以是阿里云的 RDS）。
-   构建样例工程依赖 Maven，准备一个可用的 Maven 环境。

GTS SDK 2.9.0 版本开始提供对 Seata 的兼容支持。关于 Seata 的更多信息，请参见 [Seata](https://github.com/seata/seata)

## 样例简介

样例工程模拟了资金转账的应用，包含 2 个数据源：

-   帐户 A 数据源：存储 A 的资金。
-   帐户 B 数据源：存储 B 的资金。

通过 Seata 管理的分布式事务，保障帐户 A 和 B 之间交易的一致性。

## 步骤一：下载样例工程

样例工程详情请参见 [gts-sample-seata](https://code.aliyun.com/txc-console/gts-sample-seata/repository/archive.zip?ref=master)。

## 步骤二：构建样例工程

1.  创建两个用于运行样例的数据库，分别执行工程中的 init-a.sql 和 init-b.sql 脚本，建立相关表。

2.  在样例工程根目录下，执行 build.sh（Linux） 或 build.bat（Windows） 脚本，构建工程。


## 步骤三：导入样例工程到 IDE

为了方便运行和理解，建议您把工程导入到 IDE 中。

## 步骤四：运行样例工程

运行样例工程中 Application 的 Main 方法，结合代码逻辑，查看 console 的日志输出。

## 关键配置和运行机制解读

application.properties 中，`seata.txc` 前缀的一系列配置是 GTS 关键配置，说明如下：

-   seata.txc.applicationId：请您为每个服务定义一个全局唯一的名字。这是 Seata 的原生配置，不需要修改。
-   seata.txc.txServiceGroup：Seata 的事务服务分组。这里配置为 GTS 服务实例名。
    -   在本地运行通过公网访问 GTS 服务时，请使用公共的实例 txc\_test\_public.1129\*\*\*\*3855\*\*\*\*.QD 并配合使用下面的 spring.cloud.txc.url 配置。
    -   在正式环境 ECS 上运行时，请使用您订购的 GTS 服务实例全名，并配合使用下面的 seata.txc.accessKey 和 seata.txc.accessKey 配置。
-   seata.txc.servcieEndPoint：公网访问 GTS 服务的接入地址，固定值 https://test-cs-gts.aliyuncs.com 。这个配置仅在本地公网访问时需要。
-   seata.txc.accessKey 和 seata.txc.secretKey：在阿里云环境上正式运行，这里配置您 GTS 服务实例使用者的 AK 和 SK 用于鉴权。默认是使用订购 GTS 服务实例的用户（即实例全名中间部分账号ID 对应用户）的 AK 和 SK。也可以使用 RAM 授权的用户 AK 和 SK，具体方法请参见[为 RAM 用户授权事务分组](https://help.aliyun.com/document_detail/118231.html)

