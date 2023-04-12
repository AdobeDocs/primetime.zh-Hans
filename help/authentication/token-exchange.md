---
title: 为Adobe令牌交换平台SSO令牌
description: 为Adobe令牌交换平台SSO令牌
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 2%

---


# 为Adobe令牌交换平台SSO令牌 {#exchange-a-platform-sso-token-for-an-adobe-token}

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

允许将平台SSO配置文件“交换”为Adobe令牌。

| 端点 | 已调用  </br>按 | 输入   </br>参数 | HTTP  </br>方法 | 响应 | HTTP  </br>响应 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/authn | 流应用程序</br></br>或</br></br>程序员服务 | 1.请求者（必填）</br>    </br>2.  deviceId（必需）</br>    </br>3.  mvpd（必需）</br>    </br>4.  deviceType（必需）</br>    </br>5.  SAMLResponse（必填）</br>    </br>6.  deviceUser（已弃用）</br>    </br>7.  appId（已弃用） | POST | 成功的响应将是“无内容”(204 No Content)，表示令牌已成功创建，并可用于创作流。 | 204 — 无内容   </br>400 — 错误请求 |


| 输入参数 | 描述 |
| --- | --- |
| 请求者 | 此操作有效的程序员请求者ID。 |
| deviceId | 设备ID字节。 |
| mvpd | 此操作有效的MVPD ID。 |
| deviceType | 我们尝试为其获取用户档案请求的Apple平台。  任一 **iOS** 或 **tvOS**. |
| SAMLResponse | Platform SSO返回的实际用户档案。 |
| _deviceUser_ | 设备用户标识符。 |
| _appId_ | 应用程序ID/名称。 |


