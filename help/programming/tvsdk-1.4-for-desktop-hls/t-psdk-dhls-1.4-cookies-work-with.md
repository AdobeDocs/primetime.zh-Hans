---
description: 您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、门访问等。
seo-description: 您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、门访问等。
seo-title: 使用Cookie
title: 使用Cookie
uuid: 7586a5a7-9914-403b-86a9-fbdd28664b07
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 使用Cookie{#work-with-cookies}

您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、门访问等。

下面是向密钥服务器发出请求时具有某种身份验证类型的示例：

1. 客户在浏览器中登录您的网站，并且其登录显示允许他们查看内容。
1. 您的应用程序会根据许可证服务器的期望值生成身份验证令牌。 将该值传递给TVSDK。
1. TVSDK在cookie头中设置该值。
1. 当TVSDK向密钥服务器发出请求以获取密钥以解密内容时，该请求在cookie头中包含身份验证值，因此密钥服务器知道该请求是有效的。

要使用Cookie，请执行以下操作：

1. 使用 `cookieHeaders` 中的属 `NetworkConfiguration` 性设置Cookie。 该属 `cookieHeaders` 性是一个Metadata对象，您可以向该对象添加键值对，以将其包含在Cookie头中。

   例如：

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   默认情况下，Cookie头仅随关键请求一起发送。 要发送包含所有请求的Cookie头，请将该 `NetworkConfiguration` 属性 `useCookieHeadersForAllRequests` 设置为true。

1. 要确保此功 `NetworkConfiguration` 能正常工作，请将其设置为元数据：

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. 在创建时提供上一步的元数据 `MediaResource`。

   例如，如果您使用该方 `createFromURL` 法，请输入以下信息：

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```

