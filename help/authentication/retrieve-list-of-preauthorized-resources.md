---
title: 检索预授权资源列表
description: 检索预授权资源列表
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# 检索预授权资源列表 {#retrieve-list-of-preauthorized-resources}

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

请求Adobe Primetime身份验证以获取预授权资源的列表。

有两组API:一组用于流应用程序或程序员服务，另一组用于第二屏幕Web应用程序。 本页介绍用于流应用程序或程序员服务的API。


| 端点 | 已调用  </br>按 | 输入   </br>参数 | HTTP  </br>方法 | 响应 | HTTP  </br>响应 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/preauthorize | 流应用程序</br></br>或</br></br>程序员服务 | 1.请求者（必填）</br>2.  deviceId（必需）</br>3.  资源列表（必填）</br>4.  device_info/X-Device-Info（必需）</br>5.  _deviceType_</br> 6.  _deviceUser_ （已弃用）</br>7.  _appId_ （已弃用） | GET | 包含单个预授权决策或错误详细信息的XML或JSON。 请参阅下面的示例。 | 200 — 成功</br></br>400 — 错误请求</br></br>401 — 未授权</br></br>405 — 不允许使用方法  </br></br>412 — 先决条件失败</br></br>500 — 内部服务器错误 |


| 输入参数 | 描述 |
| --- | --- |
| 请求者 | 此操作有效的程序员请求者ID。 |
| deviceId | 设备ID字节。 |
| 资源列表 | 一个字符串，其中包含以逗号分隔的resourceId列表，用于标识用户可访问且由MVPD授权端点识别的内容。 |
| device_info/</br></br>X-Device-Info | 流设备信息。</br></br>**注意**:此URL可以作为URL参数传递，但由于此参数的潜在大小以及GETURL长度的限制，它应作为X-Device-Info在http标头中传递。 </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | 设备类型（例如Roku、PC）。</br></br>如果此参数设置正确，ESM将提供 [按设备类型划分](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用无客户端时，可以执行不同类型的分析，例如Roku、AppleTV和Xbox。</br></br>看， [在传递量度中使用无客户端设备类型参数的好处&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**注意**:the `device_info` 将替换此参数。 |
| _deviceUser_ | 设备用户标识符。 |
| _appId_ | 应用程序ID/名称。 </br></br>**注意**:device_info替换此参数。 |



### 示例响应 {#sample-response}

 

**XML:**

```XML
HTTP/1.1 200 OK
Adobe-Request-Id : 7af28ec2-a068-45c2-8009-f5443049baf4
Adobe-Response-Confidence : full
Content-Type: application/xml; charset=utf-8

<resources>
  <resource>
    <id>TestStream1</id>
    <authorized>true</authorized>
  </resource>
  <resource>
    <id>TestStream2</id>
    <authorized>false</authorized>
    <error>
      <status>403</status>
      <code>authorization_denied_by_mvpd</code>
      <message>User not authorized</message>
      <details>Your subscription package does not include the "TestStream3" channel.</details>
      <helpUrl>https://experienceleague-review.corp.adobe.com/docs/primetime/authentication/auth-features/error-reportn/enhanced-error-codes.html#error-codes</helpUrl>
      <trace>0453f8c8-167a-4429-8784-cd32cfeaee58</trace>
      <action>none</action>
    </error>
  </resource>
</resources>
```
 
</br>

**JSON:**

```JSON
HTTP/1.1 200 OK
Adobe-Request-Id : 7af28ec2-a068-45c2-8009-f5443049baf4
Adobe-Response-Confidence : full
Content-Type: application/json; charset=utf-8
 
{
   "resources" : [
        {
            "id" : "TestStream1",
            "authorized" : true
        },
        {
            "id" : "TestStream3",
            "authorized" : false,
            "error" : {
               "status" : 403,
               "code" : "authorization_denied_by_mvpd",
               "message" : "User not authorized",
               "details" : "Your subscription package does not include the "TestStream3" channel.",
               "helpUrl" : "https://experienceleague-review.corp.adobe.com/docs/primetime/authentication/auth-features/error-reportn/enhanced-error-codes.html#error-codes",
               "trace" : "0453f8c8-167a-4429-8784-cd32cfeaee58",
               "action" : "none"
            }
        } 
    ]
}
```
