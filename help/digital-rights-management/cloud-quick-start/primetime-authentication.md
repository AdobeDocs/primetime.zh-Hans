---
title: Adobe Primetime身份验证（可选）
description: Adobe Primetime身份验证（可选）
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Adobe Primetime身份验证（可选） {#adobe-primetime-authentication-optional}

如果用于打包内容的DRM策略是匿名策略，则将向所有许可证请求颁发许可证。 或者，Primetime Cloud DRM还支持通过Adobe Primetime身份验证进行身份验证。 如果启用了此功能，除非客户端设备首先获得Primetime身份验证令牌并通过相应的客户端API在本地设置它，否则将不会颁发许可证( `setAuthenticationToken`)来设置自定义身份验证令牌。 有关将Primetime身份验证集成到身份验证工作流的详细信息，请参阅： [Adobe Primetime身份验证。](https://tve.helpdocsonline.com/home)

在许可证获取期间，如果DRM策略指出需要Pri时间身份验证，则许可证服务器将解析并验证Primetime身份验证短媒体令牌。 如果DRM策略指定 `ResourceID` 或 `RequestorID`，许可证服务器还将针对这些属性验证令牌。 如果未设置，则许可证服务器将在令牌验证期间将属性指定为“null”。 仅当令牌验证成功时，才会颁发许可证；否则，客户端将发送一个带有305子错误代码（用户未授权）的3328 DRMErrorEvent。

Primetime身份验证参数必须在策略中指定，该策略用于打包预定需要Primetime身份验证的内容。

相关物业包括：

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>在将Primetime身份验证与(DRM)许可证轮换功能结合使用时，请记住Primetime身份验证短媒体令牌(SMT)的有效期较短。 如果您的应用程序计划使用许可证轮换(例如，支持 *封锁* 用例)，应用程序必须意识到这一点，并在轮换其许可证之前刷新其Primetime身份验证短媒体令牌。
