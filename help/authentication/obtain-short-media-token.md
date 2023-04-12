---
title: 获取短媒体令牌
description: 获取短媒体令牌
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# 获取短媒体令牌 {#obtain-short-media-token}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## REST API端点 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 生产 —  [`api.auth.adobe.com`](http://api.auth.adobe.com/)
* 暂存 —  [`api.auth-staging.adobe.com`](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生产 —  [`api.auth.adobe.com`](http://api.auth.adobe.com/)
* 暂存 —  [`api.auth-staging.adobe.com`](http://api.auth-staging.adobe.com/)

</br>

## 描述 {#description}

获取短媒体令牌。  

| 端点 | 已调用  </br>按 | 输入   </br>参数 | HTTP  </br>方法 | 响应 | HTTP  </br>响应 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/mediatoken</br></br>  或</br></br>&lt;sp_fqdn>/api/v1/tokens/media</br></br>例如：</br></br>&lt;sp_fqdn>/api/v1/tokens/media | 流应用程序</br></br>或</br></br>程序员服务 | 1.请求者（必填）</br>2.  deviceId（必需）</br>3.  资源（必需）</br>4.  device_info/X-Device-Info（必需）</br>5.  _deviceType_</br> 6.  _deviceUser_ （已弃用）</br>7.  _appId_ （已弃用） | GET | 包含Base64编码的媒体令牌的XML或JSON，或者，如果失败，则包含错误详细信息。 | 200 — 成功  </br>403 — 无法成功 |

{style="table-layout:auto"}

<!--
| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| `<SP_FQDN>/api/v1/mediatoken`</br></br>  or</br></br>`<SP_FQDN>/api/v1/tokens/media`</br></br>For example:</br></br>`<SP_FQDN>/api/v1/tokens/media` | Streaming App</br></br>or</br></br>Programmer Service | <ol><li>requestor (Mandatory)</l><li>deviceId (Mandatory)</li><li>resource (Mandatory)</li><li>device_info/X-Device-Info (Mandatory)</li><li>_deviceType_</li><li>_deviceUser_ (Deprecated)</li><li>_appId_ (Deprecated)</li></ol> | GET | XML or JSON containing an Base64 encoded media token or error details if unsuccessful. | 200 - Success  </br>403 - No Success |
-->

</br>

| 输入参数 | 描述 |
| --- | --- |
| 请求者 | 此操作有效的程序员请求者ID。 |
| deviceId | 设备ID字节。 |
| 资源 | 包含resourceId（或MRSS片段）的字符串，用于标识用户请求的内容，并由MVPD授权端点识别。 |
| device_info/</br></br>X-Device-Info | 流设备信息。</br></br>**注意**:此URL可以作为URL参数传递，但由于此参数的潜在大小以及GETURL长度的限制，它应作为X-Device-Info在http标头中传递。 </br></br>请参阅 [传递设备和连接信息](/help/authentication/passing-client-information-device-connection-and-application.md). |
| _deviceType_ | 设备类型（例如Roku、PC）。</br></br>如果此参数设置正确，ESM将提供 [按设备类型划分]/(help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type)，以便可以针对不同类型的分析执行。 例如，Roku、AppleTV和Xbox。</br></br>请参阅 [使用无客户端设备类型参数的好处&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**注意**:device_info将替换此参数。 |
| _deviceUser_ | 设备用户标识符。</br></br>**注意**:如果使用，deviceUser的值应与 [创建注册代码](/help/authentication/registration-code-request.md) 请求。 |
| _appId_ | 应用程序ID/名称。 </br></br>**注意**:device_info替换此参数。 如果使用， `appId` 的值应与 [创建注册代码](/help/authentication/registration-code-request.md) 请求。 |

{style="table-layout:auto"}

### 示例响应 {#response}

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <play>
        <expires>1348649569000</expires>
        <mvpdId>sampleMvpdId</mvpdId>
        <requestor>sampleRequestorId</requestor>
        <resource>sampleResourceId</resource>
        <serializedToken>PHNpZ25hdH[...]</serializedToken>
        <userId>sampleScrambledUserId</userId>
    </play>
```



**JSON:**

```JSON
    {
        "resource": "sampleResourceId",
        "requestor": "sampleRequestorId",
        "expires": "1348649614000",
        "serializedToken": "PHNpZ25hdH[...]",
        "userId": "sampleScrambledUserId",
        "mvpdId": "sampleMvpdId"
    }
```

 

### 媒体验证库兼容性

字段 `serializedToken` 从“获取短媒体令牌”调用中，是可针对Adobe Medium验证库验证的Base64编码令牌。
