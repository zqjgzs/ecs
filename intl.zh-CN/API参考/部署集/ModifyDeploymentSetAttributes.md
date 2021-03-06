# ModifyDeploymentSetAttributes {#doc_api_999649 .reference}

修改一个部署集的名称和描述信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyDeploymentSetAttribute)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DeploymentSetId|String|是|ds-deploymentsetid|部署集ID。

 |
|RegionId|String|是|cn-hangzhou|部署集所属地域ID。您可以调用DescribeRegions查看最新的阿里云地域列表。

 |
|Action|String|否|ModifyDeploymentSetAttribute|系统规定参数，取值：ModifyDeploymentSetAttributes

 |
|DeploymentSetName|String|否|FinanceJoshua|新的部署集名称。长度为 2~128 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 |
|Description|String|否|FinanceDept|新的部署集描述信息。长度为 2~256 个英文或中文字符，不能以 http:// 和 https:// 开头。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifyDeploymentSetAttributes
&RegionId=cn-hangzhou
&Strategy=Availability
&DeploymentSetId=ds-bp1frxuzdg87zh4pzqkc
&DeploymentSetName=AvailMySet
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDeploymentSetAttributesResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyDeploymentSetAttributesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|The input parameter RegionId that is mandatory for processing this request is not supplied.|参数 RegionID 不得为空。|
|400|InvalidDescription.Malformed|The specified parameter Description is not valid.|指定的资源描述格式不合法。长度为2-256个字符，不能以 http:// 和 https:// 开头。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

