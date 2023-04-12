---
title: 临时通行证和促销临时通行证的免费预览
description: 临时通行证和促销临时通行证的免费预览
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---


# 临时通行证和促销临时通行证的免费预览 {#free-preview-for-temp-pass-and-promotional-temp-pass}

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

允许为临时通行证和促销临时通行证创建身份验证令牌，而无需第二个屏幕。


| 端点 | 已调用  </br>按 | 输入   </br>参数 | HTTP  </br>方法 | 响应 | HTTP  </br>响应 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authenticate/freepreview | 流应用程序</br></br>或</br></br>程序员服务 | 1.requestor_id（必填）</br>    </br>2.  deviceId（必需）</br>    </br>3.  mso_id（必填）</br>    </br>4.  domain_name（必填）</br>    </br>5.  device_info/X-Device-Info（必需）</br>6.  deviceType</br>    </br>7.  deviceUser（已弃用）</br>    </br>8.  appId（已弃用）</br>    </br>9.  generic_data（可选） | POST | 成功的响应将是“无内容”(204 No Content)，表示令牌已成功创建，并可用于创作流。 | 204 — 无内容   </br>400 — 错误请求 |

<div>


| 输入参数 | 描述 |
| --- | --- |
| requestor_id | 此操作有效的程序员请求者ID。 |
| deviceId | 设备ID字节。 |
| mso_id | 此操作有效的MVPD ID。 |
| domain_name | 将为其授予令牌的域名。 在授予授权令牌时，将与服务提供商的域进行比较。 |
| device_info/</br></br>X-Device-Info | 流设备信息。</br></br>**注意**:此URL可以作为URL参数传递，但由于此参数的潜在大小以及GETURL长度的限制，它应作为X-Device-Info在http标头中传递。 </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | 设备类型（例如Roku、PC）。</br></br>如果此参数设置正确，ESM将提供 [按设备类型划分](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用无客户端时，以便可以对Roku、AppleTV、Xbox等执行不同类型的分析。</br></br>请参阅 [使用无客户端设备类型参数的好处&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**注意**:device_info将替换此参数。 |
| _deviceUser_ | 设备用户标识符。</br></br>**注意**：如果使用，deviceUser的值应与 [创建注册代码](/help/authentication/registration-code-request.md) 请求。 |
| _appId_ | 应用程序ID/名称。 </br></br>**注意**:device_info替换此参数。 如果使用， `appId` 的值应与 [创建注册代码](/help/authentication/registration-code-request.md) 请求。 |
| generic_data | 用于限制促销临时通行证的令牌范围。 |


### [返回到REST API引用](/help/authentication/rest-api-reference.md)
