# 部署 SDK

注解使用方式需要在 GTS 客户端上部署 SDK，才能使用分布式事务。GTS SDK 目前只支持 Java 版本。

## 操作步骤

1.  下载 GTS SDK 开发包。

    建议选择 GTS SDK 最新版本，也可以根据实际需求选择其它历史版本，详情请参见[版本说明](/cn.zh-CN/产品简介/版本说明.md)。

2.  如果需要 Spring Cloud 原生支持，需要下载 [Spring Cloud 原生支持包](http://txc-console.oss-cn-beijing.aliyuncs.com/sdk/txc-client-springcloud-2.8.50.jar)。

    **说明：** 若之前从未使用过GTS或者Seata建议使用2.8.x版本；若想兼容支持开源 Seata 的功能，请在版本列表选择2.9.x的版本，若想添加Spring Cloud 的支持需要额外 spring-cloud-alibaba-seata。目前Seata 已支持多种数据库，多种 RPC 框架，详情请参见[Seata](https://github.com/seata/seata)。

3.  将 SDK SDK 开发包上传到 GTS 客户端所在的机器上。

4.  将 SDK 开发包添加到应用的依赖中。

    具体方式没有限制，这里不一一列举。

    典型的情况是：如果使用 Maven 来管理应用工程，可以将 SDK 开发包添加到 pom.xml 依赖中。

    将 SDK 开发包添加到 pom.xml 依赖中的示例如下：

    ```
    <dependency>
        <groupId>com.taobao.txc</groupId>
        <artifactId>txc-client</artifactId>
        <version>${txc-version}</version>
        <scope>system</scope>
        <systemPath>SDK的存放路径</systemPath>
    </dependency>
    ```

    使用 Spring Cloud 原生支持时，如果应用中自己定义了 WebMvcConfigurationSupport，请添加 TxcInboundHander 的实例，示例代码如下：

    ```
    public class MyWebMvcConfigurationSupport extends WebMvcConfigurationSupport {
    
        @Override
        protected void addInterceptors(InterceptorRegistry registry) {
            registry.addInterceptor(new TxcInboundHandler()).addPathPatterns(new String[] { "/**" });
    
        }
    }            
    ```


