---
description: 您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、网关访问等。
title: 使用Cookie
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# 使用Cookie{#work-with-cookies}

您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、网关访问等。

以下是在向密钥服务器发出请求时进行某种身份验证的示例：

1. 您的客户在浏览器中登录您的网站，其登录信息显示他们有权查看内容。
1. 您的应用程序会根据许可证服务器的预期生成身份验证令牌。 将该值传递给TVSDK。
1. TVSDK会在Cookie标头中设置该值。
1. 当TVSDK向密钥服务器发出获取密钥以解密内容的请求时，该请求在Cookie标头中包含身份验证值，因此密钥服务器知道该请求有效。

要使用Cookie，请执行以下操作：

1. 使用 `cookieHeaders` 中的属性 `NetworkConfiguration` 以设置Cookie。 此 `cookieHeaders` 属性是一个元数据对象，您可以将键值对添加到此对象以包含在Cookie标头中。

   例如：

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   默认情况下，Cookie标头仅随密钥请求一起发送。 要发送包含所有请求的Cookie标头，请设置 `NetworkConfiguration` 属性 `useCookieHeadersForAllRequests` 为真。

1. 为确保 `NetworkConfiguration` 工作，将其设置为元数据：

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. 创建时提供上一步骤中的元数据 `MediaResource`.

   例如，如果您使用 `createFromURL` 方法，请输入以下信息：

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```
