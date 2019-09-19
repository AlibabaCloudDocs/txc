# DescribeGtmInstanceSystemCname {#doc_api_Alidns_DescribeGtmInstanceSystemCname .reference}

调用DescribeGtmInstanceSystemCname获取系统分配的cname域名。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Alidns&api=DescribeGtmInstanceSystemCname&type=RPC&version=2015-01-09)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeGtmInstanceSystemCname|系统规定参数。取值：**DescribeGtmInstanceSystemCname**。

 |
|InstanceId|String|是|instance1|实例ID。

 |
|Lang|String|否|en|用户语言。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|6856BCF6-11D6-4D7E-AC53-FD579933522B|请求ID。

 |
|SystemCname|String|gtm-cn-mp91004xxxx.gtm-a2b4.com|系统分配cname域名。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://alidns.aliyuncs.com/?Action=DescribeGtmInstanceSystemCname
&InstanceId=instance1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeGtmInstanceSystemCnameResponse>
	  <RequestId>6856BCF6-11D6-4D7E-AC53-FD579933522B</RequestId>
	  <SystemCname>gtm-cn-mp91004xxxx.gtm-a2b4.com</SystemCname>
</DescribeGtmInstanceSystemCnameResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"6856BCF6-11D6-4D7E-AC53-FD579933522B",
	"SystemCname":"gtm-cn-mp91004xxxx.gtm-a2b4.com"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Alidns)查看更多错误码。

