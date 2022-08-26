---
title: 启动授权
description: 启动授权
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 启动授权 {#initiate-authorization}

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

获取授权响应。 

| 端点 | 已调用  </br>按 | 输入   </br>参数 | HTTP  </br>方法 | 响应 | HTTP  </br>响应 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authorize | 流应用程序</br></br>或</br></br>程序员服务 | 1.请求者（必填）</br>2.  deviceId（必需）</br>3.  资源（必需）</br>4.  device_info/X-Device-Info（必需）</br>5.  _deviceType_</br> 6.  _deviceUser_ （已弃用）</br>7.  _appId_ （已弃用）</br>8.  额外参数（可选） | GET | 包含授权详细信息或错误详细信息（如果失败）的XML或JSON。 请参阅下面的示例。 | 200 — 成功  </br>403 — 无法成功 |

{style=&quot;table-layout:auto&quot;}

</br>


| 输入参数 | 描述 |
| --- | --- |
| 请求者 | 此操作有效的程序员请求者ID。 |
| deviceId | 设备ID字节。 |
| 资源 | 包含resourceId（或MRSS片段）的字符串，用于标识用户请求的内容，并由MVPD授权端点识别。 |
| device_info/</br></br>X-Device-Info | 流设备信息。</br></br>**注意**:此URL可以作为URL参数传递，但由于此参数的潜在大小以及GETURL长度的限制，它应作为X-Device-Info在http标头中传递。 </br></br>请参阅 [传递设备和连接信息](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | 设备类型（例如Roku、PC）。</br></br>如果此参数设置正确，ESM将提供 [按设备类型划分](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) 使用无客户端时，以便可以对Roku、AppleTV、Xbox等执行不同类型的分析。</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br></br>**注意**:device_info将替换此参数。 |
| _deviceUser_ | 设备用户标识符。 |
| _appId_ | 应用程序ID/名称。 </br></br>**注意**:device_info替换此参数。 |
| 额外参数 | 调用还可以包含可启用其他功能(如：</br></br>* generic_data — 允许使用 [促销TempPass](https://tve.helpdocsonline.com/promotional-temp-pass)</br></br>示例： `generic_data=("email":"email@domain.com")` |

{style=&quot;table-layout:auto&quot;}

>[!CAUTION]
>
>**流设备IP地址**</br>
>对于客户端到服务器实施，流设备IP地址会随此调用隐式发送。  对于服务器到服务器实施，其中 **regcode** 调用由程序员服务而不是流设备进行，需要以下标头才能传递流设备IP地址：</br></br>
>
>
```
>X-Forwarded-For : <streaming\_device\_ip>
>```
>
>where `<streaming\_device\_ip>` 是流设备公共IP地址。</br></br>
>示例：</br>
>
>
```
>POST /reggie/v1/{req_id}/regcode HTTP/1.1
>X-Forwarded-For:203.45.101.20
>```


### 示例响应 {#sample-response}

* **用例1:成功**

</br>
  * **XML:**
  </br>
    "'XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <authorization>
    <expires>1348148289000</expires>
    <mvpd>示例MvpdId</mvpd>
    <requestor>sampleRequestorId</requestor>
    <resource>sampleResourceId</resource>
    </authorization>
    "



* **JSON:**

   ```JSON
   {
     "mvpd": "sampleMvpdId",
     "resource": "sampleResourceId",
     "requestor": "sampleRequestorId",
     "expires": "1348148289000"
   }
   ```

>[!IMPORTANT]
>
>当响应来自代理MVPD时，它可能包含一个名为 `proxyMvpd`. 

 

* **用例2:拒绝授权**


   ```JSON
   <error>
     <status>403</status>
     <message>User not authorized</message>
     <details>Your subscription package does not include the "ASFAFD" channel.
     Please go to http://www.ca.ble/upgrade in order to upgrade your subscription.</details>
   </error>
   ```

[返回到REST API引用](http://tve.helpdocsonline.com/rest-api-reference)
