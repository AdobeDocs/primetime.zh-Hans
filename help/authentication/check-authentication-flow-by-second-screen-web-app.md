---
title: 通过第二屏幕Web应用程序检查身份验证流程
description: 通过第二屏幕Web应用程序检查身份验证流程
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 通过第二屏幕Web应用程序检查身份验证流程 {#check-authentication-flow-by-second-screen-web-app}

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

第二个屏幕登录Web应用程序应使用此API，以确认Adobe Primetime身份验证已确认从MVPD成功登录。 我们建议在向最终用户显示成功消息之前调用此API，该消息会指示他/她继续到设备控制台以继续工作流。


| 端点 | 已调用  </br>按 | 输入   </br>参数 | HTTP  </br>方法 | 响应 | HTTP  </br>响应 |
| --- | --- | --- | --- | --- | --- |
| SP_FQDN/api/v1/checkauthn/{注册代码} | 登录Web应用程序 | 1.注册码  </br>    （路径组件）</br>2.  请求者  </br>    （必需） | GET | XML或JSON，其中包含错误详细信息（如果失败）。 | 200 — 成功   </br>403 — 禁止 |

</br>

| 输入参数 | 描述 |
| ----------------- | --------------------------------------------------------------------------------------------- |
| 注册码 | 用户在验证流程的开头提供的注册代码值。 |
| 请求者 | 此操作有效的程序员请求者ID。 |


### 示例响应（如果出错） {#response}

```JSON
    {
        "status": 403,
        "message": "Forbidden"
    }
```

### [返回到REST API引用](/help/authentication/rest-api-reference.md)
