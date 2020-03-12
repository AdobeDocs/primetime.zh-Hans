---
description: 您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、门访问等。
seo-description: 您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、门访问等。
seo-title: 使用Cookie
title: 使用Cookie
uuid: f060b520-ceec-48ca-929f-683566fe6ae7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 使用Cookie{#work-with-cookies}

您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、门访问等。

下面是向密钥服务器发出请求时具有某种身份验证类型的示例：

1. 客户在浏览器中登录您的网站，并且其登录显示允许他们查看内容。
1. 您的应用程序会根据许可证服务器的期望值生成身份验证令牌。 将该值传递给TVSDK。
1. TVSDK在cookie头中设置该值。
1. 当TVSDK向密钥服务器发出请求以获取密钥以解密内容时，该请求在cookie头中包含身份验证值，因此密钥服务器知道该请求是有效的。

要使用Cookie，请执行以下操作：

1. 创建 `cookieManager` 并将URI的Cookie添加到您的 `cookieStore`。

   例如：

   >[!IMPORTANT]
   >
   >启用302重定向后，广告请求可被重定向到不同于cookie所属域的域。

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   TVSDK在运行时查询此cookieManager，检查是否有任何与URL关联的cookie，并自动使用这些cookie。

   另一个选项是在中 `cookieHeaders` 使用 `NetworkConfiguration` 设置用于请求的任意cookie头字符串。 默认情况下，此Cookie头仅随密钥请求一起发送。 要发送包含所有请求的Cookie头，请使用以下 `NetworkConfiguration` 方法 `setUseCookieHeadersForAllRequests`:

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

