---
title: 检查身份验证令牌
description: 检查身份验证令牌
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---


# 检查身份验证令牌 {#check-authentication-token}

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

指示设备是否具有未过期的身份验证令牌。

| 端点 | 已调用  </br>按 | 输入   </br>参数 | HTTP  </br>方法 | 响应 | HTTP  </br>响应 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/checkauthn | 流应用程序</br></br>或</br></br>程序员服务 | 1.请求者（必填）</br>2.  deviceId（必需）</br>3.  device_info/X-Device-Info（必需）</br>4.  _deviceType_ </br>5.  _deviceUser_ （已弃用）</br>6.  _appId_ （已弃用） | GET | XML或JSON，其中包含错误详细信息（如果失败）。 | 200 — 成功   </br>403 — 无法成功 |

{style=&quot;table-layout:auto&quot;}


| 输入参数 | 描述 |
| --- | --- |
| 请求者 | 此操作有效的程序员请求者ID。 |
| deviceId | 设备ID字节。 |
| device_info/</br></br>X-Device-Info | 流设备信息。</br></br>**注意**:此URL可以作为URL参数传递，但由于此参数的潜在大小以及GETURL长度的限制，它应作为X-Device-Info在http标头中传递。 </br></br>请参阅 [传递设备和连接信息](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | 设备类型（例如Roku、PC）。</br></br>如果此参数设置正确，ESM将提供 [按设备类型划分](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) 使用无客户端时，以便可以对Roku、AppleTV、Xbox等执行不同类型的分析。</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br>**注意**:device_info将替换此参数。 |
| _deviceUser_ | 设备用户标识符。 |
| _appId_ | 应用程序ID/名称。</br>**注意**:device_info替换此参数。 |

{style=&quot;table-layout:auto&quot;}


## 响应（如果失败） {#response}

```JSON
    <error>
      <status>403</status>
      <message>Authentication token expired</message>
    </error>
```

### [返回到REST API引用](http://tve.helpdocsonline.com/rest-api-reference)
