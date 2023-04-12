---
title: 启动注销
description: 启动注销
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# 启动注销 {#initiate-logout}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## REST API端点 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 生产 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暂存 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生产 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暂存 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## 描述 {#description}

从存储中删除AuthN和AuthZ令牌。


| 端点 | 已调用  </br>按 | 输入   </br>参数 | HTTP  </br>方法 | 响应 | HTTP  </br>响应 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/logout | 流应用程序</br></br>或</br></br>程序员服务 | 1.请求者</br>2.  deviceId（必需）</br>3.  device_info/X-Device-Info（必需）</br>4.  _deviceType_</br> 5.  _deviceUser_ （已弃用）</br>6.  _appId_ （已弃用） | DELETE | 无 | 204 |


| 输入参数 | 描述 |
| --- | --- |
| 请求者 | 此操作有效的程序员请求者ID。 |
| deviceId | 设备ID字节。 |
| device_info/</br></br>X-Device-Info | 流设备信息。</br></br>**注意**:此URL可以作为URL参数传递，但由于此参数的潜在大小以及GETURL长度的限制，它应作为X-Device-Info在http标头中传递。 </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | 设备类型（例如Roku、PC）。</br></br>如果此参数设置正确，ESM将提供 [按设备类型划分](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用无客户端时，以便可以对Roku、AppleTV、Xbox等执行不同类型的分析。</br></br>请参阅 [在传递量度中使用无客户端设备类型参数的好处&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**注意**:device_info将替换此参数。 |
| _deviceUser_ | 设备用户标识符。</br></br>**注意**：如果使用，deviceUser的值应与 [创建注册代码](/help/authentication/registration-code-request.md) 请求。 |
| _appId_ | 应用程序ID/名称。 </br></br>**注意**:device_info替换此参数。 如果使用， `appId` 的值应与 [创建注册代码](/help/authentication/registration-code-request.md) 请求。 |

>[!IMPORTANT]
> 
>注销呼叫当前具有以下限制：它会从存储中清除AuthN和AuthZ令牌（即，在程序员/Primetime身份验证端），但 **不** 调用MVPD注销端点。 


