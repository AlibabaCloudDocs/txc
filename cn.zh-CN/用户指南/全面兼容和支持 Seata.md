# 全面兼容和支持 Seata

GTS 已经全面兼容和支持开源分布式事务 Seata，实现与 Seata 的协议兼容，支持使用 Seata 的应用无缝迁移到云上，基于 GTS 提供的服务高效运行。

## Seata 简介

Simple Extensible Autonomous Transaction Architecture（Seata）是一款开源的分布式事务解决方案，致力于提供高性能和简单易用的分布式事务服务。

2019 年，基于 GTS 的技术积累，阿里巴巴发起了开源项目 [Seata](https://github.com/seata/seata?spm=a2c4g.11186623.2.12.102873de9SDqld)。

2020 年 2 月，基于 Seata 项目 GA 后的版本，GTS 实现与 Seata 的协议兼容，支持使用 Seata 的应用无缝迁移到云上，基于 GTS 提供的服务高效运行。

![Seata Roadmap](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3919119951/p88927.png)

## 分布式事务框架和事务模式

GTS 和 Seata 定义的分布式事务框架是完全一致的，详情请参见[分布式事务框架和事务模式](/cn.zh-CN/用户指南/分布式事务框架和事务模式.md)。

TM、RM 和应用部署在一起，应用根据业务需求，选择合适的分布式事务模式来解决数据一致性问题。

无论使用哪处模式，都离不开一个稳定高效的 TC 提供服务。这些服务包括（但不限于）：

-   记录全局事务状态
-   记录事务分支的注册
-   驱动事务分支进行最终的提交或回滚
-   事务链路监控
-   异常事务的恢复
-   全局事务超时检测
-   全局事务间隔离机制

分布式事务的协调机制被定义为一项标准化的服务，独立部署和运维，给应用的分布式系统提供事务服务。

## 协议和架构

基于事务框架定义的事务协议如下图所示。

![Seata 和 GTS 事务协议](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3919119951/p88929.png)

Seata 的分布式事务框架源自 GTS，二者的底层架构和事务协议是完全一致的。

-   GTS 把 TM 和 RM 的实现统一打包到 GTS SDK（GTS Client） 中。
-   GTS 服务端（GTS Server）就是 TC 的一个高可用实现。

依托于阿里云的基础设施，GTS Server 以多副本、高可用集群形态部署，提供高质量的事务协调服务。

## 将 Seata 应用迁移到 GTS

架构和协议层面一致，使得 GTS 可以很自然地提供对 Seata 应用的事务协调支持。只要实现具体网络通信机制上的兼容适配，就可以完整支撑 Seata 应用运行在 GTS 服务之上。

Seata 应用迁移到云上使用 GTS 服务不需要做任何编程改造，仅仅是把自运维的 Seata 的 TC Server 替换为 GTS 提供的高性能、高可靠、高可用的云服务。

![Seata 应用迁移上云](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3919119951/p88963.png)

GTS 的 SDK 2.9.0 版本支持基于 Seata 的应用使用 AT 模式，运行在 GTS 服务上。详情请参见 [Seata 应用样例](/cn.zh-CN/用户指南/AT 模式/样例工程/Seata 应用样例.md)。

