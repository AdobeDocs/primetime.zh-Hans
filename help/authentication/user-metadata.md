---
title: 用户元数据
description: 用户元数据
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 用户元数据 {#user-metadata}

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

检索MVPD共享的有关已验证用户的元数据。

<div>


| 端点 | 已调用  </br>按 | 输入   </br>参数 | HTTP  </br>方法 | 响应 | HTTP  </br>响应 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/usermetadata | 流应用程序</br></br>或</br></br>程序员服务 | 1.请求者</br>2.  deviceId（必需）</br>3.  device_info/X-Device-Info（必需）</br>4.  deviceType</br>5.  deviceUser（已弃用）</br>6.  appId（已弃用） | GET | 包含用户元数据或错误详细信息（如果失败）的XML或JSON。 | 200 — 成功</br></br>404 — 未找到元数据</br></br>412 — 无效的AuthN令牌（例如，过期的令牌） |


| 输入参数 | 描述 |
| --- | --- |
| 请求者 | 此操作有效的程序员请求者ID。 |
| deviceId | 设备ID字节。 |
| device_info/</br></br>X-Device-Info | 流设备信息。</br></br>**注意**:此URL可以作为URL参数传递，但由于此参数的潜在大小以及GETURL长度的限制，它应作为X-Device-Info在http标头中传递。 </br></br>请参阅 [传递设备和连接信息](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | 设备类型（例如Roku、PC）。</br></br>如果此参数设置正确，ESM将提供 [按设备类型划分](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) 使用无客户端时，以便可以对Roku、AppleTV、Xbox等执行不同类型的分析。</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br></br>**注意**:device_info将替换此参数。 |
| _deviceUser_ | 设备用户标识符。</br></br>**注意**：如果使用，deviceUser的值应与 [创建注册代码](http://tve.helpdocsonline.com/registration-code-request) 请求。 |
| _appId_ | 应用程序ID/名称。 </br></br>**注意**:device_info替换此参数。 如果使用， `appId` 的值应与 [创建注册代码](http://tve.helpdocsonline.com/create-registration-page-/-login-uri) 请求。 |

>[!NOTE]
> 
>用户元数据信息应在验证流程完成后可用，但可以根据授权流程进行更新，具体取决于MVPD和元数据类型。

</br>

## 示例响应 {#sample-response}

成功调用后，服务器将使用XML（默认）或JSON对象做出响应，该对象的结构与下面所示的类似：

```JSON
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
              zip: ["12345", "34567"],
              maxRating: { 
                  "MPAA": "PG-13",
                  "VCHIP": "TV-Y", 
                  "URL": "http://exam.pl/e/manage/ratings"
              },
              householdID: "3456",
              userID: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
              channelID: ["channel-1", "channel-2"]
    }
```

 

对象的根将有三个节点：

* *更新*:指定表示上次更新元数据的时间的UNIX时间戳。 在身份验证阶段期间生成元数据时，此属性最初将由服务器设置。 后续调用（更新元数据后）将导致时间戳递增。

* *数据*:包含实际元数据值。 

* *加密*:列出加密属性的数组。 要解密特定的元数据值，程序员必须对元数据执行Base64解码，然后对结果值应用RSA解密，并使用它自己的私钥(Adobe使用程序员的公共证书对服务器上的元数据进行加密)。

如果出现错误，服务器将返回一个XML或JSON对象，该对象指定详细的错误消息。

**更多信息：** [用户元数据](http://tve.helpdocsonline.com/user-metadata-v2)


### [返回到REST API引用](http://tve.helpdocsonline.com/rest-api-reference)
