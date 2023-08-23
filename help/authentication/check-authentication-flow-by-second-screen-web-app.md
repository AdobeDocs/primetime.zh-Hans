---
title: 通过第二屏幕Web应用程序检查身份验证流程
description: 通过第二屏幕Web应用程序检查身份验证流程
exl-id: 5807f372-a520-4069-b837-67ae41b7f79b
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# 通过第二屏幕Web应用程序检查身份验证流程 {#check-authentication-flow-by-second-screen-web-app}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权使用。

## REST API端点 {#clientless-endpoints}

&lt;reggie_fqdn>：

* 生产 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暂存 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>：

* 生产 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暂存 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## 描述 {#description}

此API应由第二个屏幕登录Web应用程序使用，以确认Adobe Primetime身份验证已确认从MVPD成功登录。 我们建议先调用此API，然后再向最终用户显示一条成功消息，指示他/她继续进入设备控制台以继续执行工作流。


| 端点 | 已调用  </br>按 | 输入   </br>参数 | HTTP  </br>方法 | 响应 | HTTP  </br>响应 |
| --- | --- | --- | --- | --- | --- |
| SP_FQDN/api/v1/checkauthn/{注册码} | 登录Web应用程序 | 1.注册码  </br>    （路径组件）</br>2.  请求者  </br>    （必需） | GET | 如果失败，则包含错误详细信息的XML或JSON。 | 200 — 成功   </br>403 — 禁止访问 |

</br>

| 输入参数 | 描述 |
| ----------------- | --------------------------------------------------------------------------------------------- |
| 注册码 | 用户在身份验证流程开始时提供的注册代码值。 |
| 请求者 | 此操作有效的程序员requestorId。 |


### 示例响应（发生错误时） {#response}

```JSON
    {
        "status": 403,
        "message": "Forbidden"
    }
```

### [返回REST API参考](/help/authentication/rest-api-reference.md)
