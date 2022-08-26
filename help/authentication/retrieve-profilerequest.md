---
title: 检索Platform SSO配置文件请求
description: 检索Platform SSO配置文件请求
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# 检索Platform SSO配置文件请求 {#retrieve-platform-sso-profile-request}

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

此资源为请求者ID和MVPD元组生成配置文件请求。


| 端点 | 已调用  </br>按 | 输入   </br>参数 | HTTP  </br>方法 | 响应 | HTTP  </br>响应 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/{requestor}/profile-requests/{mvpd} | 流应用程序</br></br>或</br></br>程序员服务 | 1.请求者(path param)</br>2. mvpd（路径参数）</br>3. deviceType（必需） | GET | 响应Content-Type将为application/八位字节流，因为客户端应用程序的实际负载是不透明的。</br></br>应用程序应将响应转发到平台</br></br>用于获取用户档案SSO的SSO引擎。 | 200 — 成功   </br>400 — 错误请求 |


| 输入参数 | 描述 |
| --------------- | -------------------------------------------------------------------------------------------------------- |
| 请求者 | 此操作有效的程序员请求者ID。 |
| mvpd | 此操作有效的MVPD ID。 |
| deviceType | 我们尝试为其获取用户档案请求的Apple平台。  任一 **iOS** 或 **tvOS**. |

### [返回到REST API引用](http://tve.helpdocsonline.com/rest-api-reference)
