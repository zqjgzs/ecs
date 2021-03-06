# ModifyInstanceNetworkSpec {#doc_api_1072927 .reference}

Modifies the bandwidth configurations of an ECS instance. When the network specifications of an instance cannot meet your needs, you can modify its bandwidth configurations to improve network performance.

## Description {#description .section}

When you call this operation, note that:

-   When modifying the bandwidth configurations of a prepaid instance, you can perform the following operations:
    -   When outbound bandwidth to the Internet is upgraded from 0 Mbit/s to a non-zero value, a public IP address is automatically allocated.
    -   You can use this API to change the bandwidth billing method from PayByTraffic to PayByBandwidth. You can use [ECS console](https://ecs.console.aliyun.com) to change the bandwidth billing method from PayByTraffic to PayByBandwidth.
-   When modifying the bandwidth configurations of a postpaid instance, you can perform the following operations:
    -   You can upgrade or downgrade the bandwidth.
    -   When outbound bandwidth to the Internet is upgraded from 0 Mbit/s to a non-zero value, a public IP address is automatically allocated. You need to call [AllocatePublicIpAddress](~~25544~~) to assign a public IP address to an instance.
-   For a classic instance, when outbound bandwidth to the Internet is upgraded from 0 Mbit/s to a non-zero value, the instance must be in the Stopped state.
-   After the bandwidth is upgraded, AutoPay is set to true by default. Make sure that your account has sufficient balance. Otherwise, your order becomes invalid and you have to cancel this order. If your account balance is insufficient, you can set the AutoPay parameter to false to generate a normal order. Then, you can log on to the [ECS console](https://ecs.console.aliyun.com) to pay for the order.
-   You can downgrade instance type for each prepaid instance three times at most, because the refund of price difference cannot exceed three times.
-   The price difference will be refunded to your original form of payment. Used coupons cannot be refunded.
-   Each time a downgrade operation is successful, you cannot perform another operation on that instance within five minutes.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceNetworkSpec) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-xxxxx1| The ID of the instance for which you want to modify network configurations.

 |
|Action|String|No|ModifyInstanceNetworkSpec| The operation that you want to perform. Set the value to ModifyInstanceNetworkSpec.

 |
|AllocatePublicIp|Boolean|No|false| Indicates whether to allocate a public IP address. Default value: false.

 |
|AutoPay|Boolean|No|true| Indicates whether to enable AutoPay. Valid values:

 -   true: After the bandwidth is upgraded, AutoPay is enabled. Make sure that your account has sufficient balance. Otherwise, your order becomes invalid and you have to cancel this order.
-   false: After the bandwidth is upgraded, an order is generated and fees are not deducted. If your account balance is insufficient, you can set the AutoPay parameter to false to generate a normal order. Then, you can log on to the [ECS console](https://ecs.console.aliyun.com) to pay for the order.

 Default value: true.

 |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000| A client token. It is used to ensure the idempotency of requests. The value of this parameter is generated by the client and is unique among different requests. It can be a maximum of 64 characters in length. For more information, see [How to ensure idempotency](~~25693~~).

 |
|EndTime|String|No|2017-12-06T22Z| The time when bandwidth update ends. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddThhZ.

 |
|InternetMaxBandwidthIn|Integer|No|10| The maximum inbound bandwidth from the Internet. Unit: Mbit/s. Valid values: 1 to 200.

 |
|InternetMaxBandwidthOut|Integer|No|10| The maximum outbound bandwidth to the Internet. Unit: Mbit/s. Valid values: 0 to 100.

 |
|NetworkChargeType|String|No|PayByTraffic| The bandwidth billing method. Valid values:

 -   PayByTraffic: traffic-based billing method.

 |
|StartTime|String|No|2017-12-05T22:40Z| The time when bandwidth upgrade starts. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddThh:mmZ.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|OrderId|String|1111111111111111111111110| The ID of the generated order.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the API request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyInstanceNetworkSpec
&RegionId=cn-hangzhou 
&InstanceId=i-xxxxx1
&InternetMaxBandwidthOut=10
&ClientToken=xxxxxxxxxxxxxx
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyInstanceNetworkSpecResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceNetworkSpecResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes {#section_6sq_vl5_c4y .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidInternetMaxBandwidthIn.ValueNotSupported|The specified InternetMaxBandwidthIn is beyond the permitted range.|The error message returned when the specified InternetMaxBandwidthIn parameter is invalid.|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified InternetMaxBandwidthOut is beyond the permitted range.|The error message returned when the specified InternetMaxBandwidthOut parameter is invalid.|
|403|IncorrectInstanceStatus|The current state of the instance does not support this operation.|The error message returned when this operation is not supported under the instance state.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned when the subscription of the instance has expired. You must renew the subscription before proceeding.|
|403|ChargeTypeViolation|The operation is not permitted due to billing method of the instance.|The error message returned when the billing method of the instance is not supported.|
|400|OperationDenied|Specified instance is in VPC.|The error message returned when the specified instance is VPC-connected.|
|400|InvalidParameter.Bandwidth|%s|The error message returned when the parameter value is invalid.|
|400|InvalidParameter.Conflict|%s|The error message returned when parameter values conflict.|
|400|InvalidStartTime.ValueNotSupported|%s|The error message returned when the end time precedes the start time.|
|400|Account.Arrearage|Your account has an outstanding payment.|The error message returned when outstanding orders exist in your account.|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is invalid.|The error message returned when the specified bandwidth billing method is invalid.|
|400|DecreasedBandwidthNotAllowed|%s|The error message returned when the bandwidth cannot be downgraded.|
|400|BandwidthUpgradeDenied.EipBoundInstance|The specified VPC instance has bound EIP, temporary bandwidth upgrade is denied.|The error message returned when the instance cannot be upgraded because it is bound with an EIP.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned when your account balance is insufficient. You need to top up your account before proceeding.|
|403|InvalidInstance.UnpaidOrder|The specified Instance has unpaid order.|The error message returned when outstanding orders exist in your account. You need to pay for the orders before proceeding.|
|400|IpAllocationError|Allocate public ip failed.|The error message returned when allocation of public IP addresses fails.|
|400|InvalidParam.AllocatePublicIp|The specified param AllocatePublicIp is invalid.|The error message returned when the specified AllocatePublicIp parameter is invalid.|
|400|InstanceDowngrade.QuotaExceed|Quota of instance downgrade is exceed.|The error message returned when the instance has been downgraded the allowed times.|
|400|InvalidBandwidth.ValueNotSupported|Instance upgrade bandwidth of temporary not allow less then existed.|The error message returned when you select a lower bandwidth for instance update.|
|403|InvalidInstance.InstanceNotSupported|The special vpc instance with eip not need bandwidth.|The error message returned when you specify the bandwidth for a VPC-connected instance bound with an EIP.|
|400|InvalidInstanceStatus|The specified instance state does not support this action.|The error message returned when this operation is not supported under the instance state.|
|403|InvalidInstanceStatus|The current state of the instance does not support this operation.|The error message returned when this operation is not supported under the instance state.|
|400|InvalidInstance.UnpaidOrder|Unpaid order exists in your account, please complete or cancel the payment in the expense center.|The error message returned when outstanding orders exist in your account.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

