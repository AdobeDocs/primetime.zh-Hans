---
description: 您可以使用TVSDK在Cookie标头中发送任意数据以进行会话管理、进行门访问等。
seo-description: 您可以使用TVSDK在Cookie标头中发送任意数据以进行会话管理、进行门访问等。
seo-title: 使用Cookie
title: 使用Cookie
uuid: 7586a5a7-9914-403b-86a9-fbdd28664b07
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# 使用cookie{#work-with-cookies}

您可以使用TVSDK在Cookie标头中发送任意数据以进行会话管理、进行门访问等。

下面是一个在向密钥服务器发出请求时具有某种身份验证类型的示例：

1. 客户在浏览器中登录您的网站，其登录表明允许他们视图内容。
1. 您的应用程序根据许可证服务器期望的内容生成身份验证令牌。 将该值传递给TVSDK。
1. TVSDK在cookie头中设置该值。
1. 当TVSDK向密钥服务器请求获取密钥以解密内容时，该请求在cookie头中包含身份验证值，因此密钥服务器知道该请求有效。

要使用Cookie:

1. 使用`NetworkConfiguration`中的`cookieHeaders`属性设置cookie。 `cookieHeaders`属性是Metadata对象，您可以向此对象添加键值对，以将其包含在Cookie头中。

   例如：

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   默认情况下，Cookie头仅随密钥请求一起发送。 要发送包含所有请求的Cookie头，请将`NetworkConfiguration`属性`useCookieHeadersForAllRequests`设置为true。

1. 要确保`NetworkConfiguration`正常工作，请将其设置为元数据：

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. 创建`MediaResource`时，请提供上一步的元数据。

   例如，如果使用`createFromURL`方法，请输入以下信息：

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```

