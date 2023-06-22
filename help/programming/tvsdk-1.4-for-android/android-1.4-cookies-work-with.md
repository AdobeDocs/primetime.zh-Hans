---
description: 您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、网关访问等。
title: 使用Cookie
exl-id: 7482777a-c338-4e0d-b123-ce2712657b8d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# 使用Cookie{#work-with-cookies}

您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、网关访问等。

在向密钥服务器发出请求时，以下是某种身份验证类型的示例：

1. 您的客户在浏览器中登录到您的网站，他们的登录信息显示他们有权查看内容。
1. 您的应用程序会根据许可证服务器的预期生成身份验证令牌。 将该值传递给TVSDK。
1. TVSDK会在Cookie标头中设置该值。
1. 当TVSDK向密钥服务器发出获取密钥以解密内容的请求时，该请求在Cookie标头中包含身份验证值，因此密钥服务器知道该请求有效。

要使用Cookie，请执行以下操作：

1. 创建 `cookieManager` 并将URI的Cookie添加到 `cookieStore`.

   例如：

   >[!IMPORTANT]
   >
   >启用302重定向后，广告请求可能会被重定向到与Cookie所属的域不同的域。

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   TVSDK在运行时查询此CookieManager，检查是否存在与该URL关联的任何Cookie，并自动使用它们。

   另一个选项是使用 `cookieHeaders` 在 `NetworkConfiguration` 以设置用于请求的任意Cookie标头字符串。 默认情况下，此Cookie标头仅随关键请求一起发送。 要发送包含所有请求的Cookie标头，请使用 `NetworkConfiguration` 方法 `setUseCookieHeadersForAllRequests`：

```java
   NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
    
   Metadata cookie = new MetadataNode(); 
   cookie.setValue("reqPayload", “1234567”); 
   networkConfiguration.setCookieHeaders(cookie); 
   networkConfiguration.setUseCookieHeadersForAllRequests( true ); 
    
   // Set NetworkConfiguration as Metadata:                                                                   
   MetadataNode resourceMetadata = new MetadataNode(); 
   resourceMetadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(),  
                            networkConfiguration); 
    
   // Call MediaResource.createFromURL to set the metadata: 
   MediaResource resource = MediaResource.createFromURL(url, resourceMetadata); 
   // Load the resource 
   mediaPlayer.replaceCurrentItem(resource);
```
