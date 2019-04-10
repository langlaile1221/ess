# AttachLoadBalancers {#concept_85125_zh .concept}

You can call this operation to add one or more SLB instances.

## Description {#section_ocm_cdk_sfb .section}

Due to [Limits](../../../../../reseller.en-US/Limits/Limits.md#), the following conditions must be met when you add SLB instances to a scaling group.

-   An SLB instance and the scaling group must be in the same account.
-   The SLB instance and the scaling group must be in the same region.
-   The status of the SLB instance must be `Active`.
-   The SLB instance must have health check enabled and be configured with at least one listener.
-   The SLB instance and the scaling group must be in the same VPC network if both of their network types are VPC.
-   When the network type of the scaling group is VPC, the network type of the SLB instance is classic. The backend server of the SLB instance includes a VPC instance, and the VPC instance and scaling group must be in the same VPC network.
-   The number of SLB instances that you add to a scaling group must be less than the quota of the scaling group.

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set the value to`AttachLoadBalancers`.|
|ScalingGroupId|String|Yes|The ID of the scaling group.|
|LoadBalancer.N|String|Yes|The ID of the SLB instance. You can add up to five SLB instances at one time.|
|ForceAttach|Boolean|No|Indicates whether to add all ECS instances in the scaling group to the backend server of the SLB instance. -    `true`: adds all ECS instances.
-    `false`: does not add all ECS instances.

Default value: `false`.|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The GUID generated by Alibaba Cloud for the request.|

## Examples { .section}

Sample requests

```
http://ess.aliyuncs.com/?Action=AttachLoadBalancers
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ 
&LoadBalancer. 1=lb-2zeur05gfsge6n
& <Common request parameters>
```

Successful response examples

`XML` format

```
<AttachLoadBalancersResponse>
    <RequestId>DD0309B7-2613-4792-9B86-275906695253</RequestId> 
</AttachLoadBalancersResponse>
```

`JSON` format

```
{
    "RequestId": "DD0309B7-2613-4792-9B86-275906695253"
}
```

## Error codes { .section}

For more information about common errors, see [Client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [Server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|HttpCode|Error code|Error message|Description|
|--------|:---------|:------------|:----------|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|The error message returned when you are not granted full permissions to call open APIs for Auto Scaling.|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|The error message returned when the specified scaling group does not exist in the account.|
|400|QuotaExceeded.LoadBalancer|LoadBalancer quota exceeded in the scaling group "%s".|The error message returned when the number of SLB instances in the scaling group exceeds the quota.|
|404|InvalidLoadBalancerId.NotFound|The load balancer "%s" does not exist.|The error message returned when the specified SLB instance does not exist.|
|400|InvalidLoadBalancerId.RegionMismatch|The load balancer "%s" and the specified scaling group are not in the same Region.|The error message returned when an SLB instance and the scaling group are not in the same region.|
|400|IncorrectLoadBalancerStatus|The current status of the load balancer "%s" does not support this action.|The error message returned when the specified operation is not supported by an SLB instance in the current status.|
|400|IncorrectLoadBalancerHealthCheck|The current health check type of the load balancer "%s" does not support this action.|The error message returned when the health check is not enabled for the specified SLB instance.|
|400|InvalidLoadBalancerId.VPCMismatch|The specified virtual switch and the instance in the load balancer "%s" are not in the same VPC.|The error message returned when an SLB instance and the scaling group are not in the same VPC network.|
|400|QuotaExceeded.BackendServer|Backend server quota exceeded in the load balancer "%s".|The error message returned when the number of backend servers of the SLB instance exceeds the quota.|
|404|InvalidScalingConfigurationId.NotFound|The specified scaling configuration does not exist.|The error message returned when the specified scaling configuration that is enabled for the current scaling group does not exist.|
