# AddGtmAccessStrategy {#doc_api_Alidns_AddGtmAccessStrategy .reference}

调用AddGtmAccessStrategy根据传入参数新增访问策略。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Alidns&api=AddGtmAccessStrategy&type=RPC&version=2015-01-09)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AccessLines|String|是|\["default", "drpeng"\]|访问区域LineCode列表。

 |
|Action|String|是|AddGtmAccessStrategy|系统规定参数。取值：**AddGtmAccessStrategy**。

 |
|DefaultAddrPoolId|String|是|hrsix|默认访问地址池ID。

 |
|FailoverAddrPoolId|String|是|hrsyw|Failover地址池ID。

 若未设置Failover地址池，传值**Empty**。

 |
|InstanceId|String|是|instance1|实例ID。

 |
|StrategyName|String|是|访问策略测试|策略名称。

 |
|Lang|String|否|en|用户语言。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|29D0F8F8-5499-4F6C-9FDC-1EE13BF55925|请求ID。

 |
|StrategyId|String|strategyid|策略ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://alidns.aliyuncs.com/?Action=AddGtmAccessStrategy
&AccessLines=["default", "drpeng"]
&DefaultAddrPoolId=hrsix
&FailoverAddrPoolId=hrsyw
&InstanceId=instance1
&StrategyName=访问策略测试
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AddGtmAccessStrategyResponse>
      <StrategyId>xxxx</StrategyId>
	  <RequestId>29D0F8F8-5499-4F6C-9FDC-1EE13BF55925</RequestId>
</AddGtmAccessStrategyResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"29D0F8F8-5499-4F6C-9FDC-1EE13BF55925",
	"StrategyId":"xxxx"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Alidns)查看更多错误码。

