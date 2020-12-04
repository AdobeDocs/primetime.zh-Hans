---
seo-title: Adobe Primetime身份验证（可选）
title: Adobe Primetime身份验证（可选）
uuid: fa6225d6-e0e5-4fcc-ac26-4ff54f9f334a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---


# Adobe Primetime身份验证（可选）{#adobe-primetime-authentication-optional}

如果用于打包内容的DRM策略是匿名策略，则将向所有许可证请求颁发许可证。 或者，Primetime Cloud DRM还支持通过Adobe Primetime身份验证进行身份验证。 如果启用此功能，则除非客户端设备首先获得Primetime身份验证令牌并通过相应的客户端API(`setAuthenticationToken`)在本地设置它以设置自定义身份验证令牌，否则将不颁发许可证。 有关将Primetime身份验证集成到身份验证工作流程中的更多信息，请参阅：[Adobe Primetime身份验证](https://tve.helpdocsonline.com/home)

在获取许可证期间，如果DRM策略声明需要Primetime身份验证，则许可证服务器将分析并验证Primetime身份验证短媒体令牌。 如果DRM策略指定了`ResourceID`或`RequestorID`，则许可证服务器还将根据这些属性验证令牌。 如果未设置，则许可证服务器将在令牌验证期间将属性指定为“null”。 只有令牌验证成功，才会颁发许可证；否则，客户端将调度3328 DRMErrorEvent，该事件具有305个子错误代码（用户未授权）。

Primetime身份验证参数必须在用于打包目标需要Primetime身份验证的内容的策略中指定。

相关物业包括：

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>在结合(DRM)许可证轮换功能使用Primetime身份验证时，请牢记Primetime身份验证短媒体令牌(SMT)的有效期较短。 如果您的应用程序计划使用许可证轮替（例如，支持&#x200B;*封锁*&#x200B;用例），则在轮替许可证之前，应用程序必须知道并刷新其Primetime身份验证短媒体令牌。