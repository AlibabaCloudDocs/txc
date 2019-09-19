# RollbackGtmRecoveryPlan {#doc_api_Alidns_RollbackGtmRecoveryPlan .reference}

调用RollbackGtmRecoveryPlan回滚容灾预案。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Alidns&api=RollbackGtmRecoveryPlan&type=RPC&version=2015-01-09)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RollbackGtmRecoveryPlan|系统规定参数。取值：**RollbackGtmRecoveryPlan**。

 |
|RecoveryPlanId|Long|是|100|容灾预案ID

 |
|Lang|String|否|en|用户语言

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|853805EA-3D47-47D5-9A1A-A45C24313ABD|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://alidns.aliyuncs.com/?Action=RollbackGtmRecoveryPlan
&RecoveryPlanId=100
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RollbackGtmRecoveryPlanResponse>
  <RequestId>853805EA-3D47-47D5-9A1A-A45C24313ABD</RequestId>
</RollbackGtmRecoveryPlanResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"6856BCF6-11D6-4D7E-AC53-FD579933522B"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Alidns)查看更多错误码。

