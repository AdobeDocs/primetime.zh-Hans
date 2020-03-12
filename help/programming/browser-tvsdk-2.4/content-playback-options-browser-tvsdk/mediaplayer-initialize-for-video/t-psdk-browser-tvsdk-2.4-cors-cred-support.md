---
description: XMLHttpRequests中对withCredentials属性的支持允许跨源资源共享(CORS)请求包含针对各种请求类型的目标域的cookie。
keywords: CORS;cross origin;resource sharing;cookies;withCredentials
seo-description: XMLHttpRequests中对withCredentials属性的支持允许跨源资源共享(CORS)请求包含针对各种请求类型的目标域的cookie。
seo-title: 跨源资源共享
title: 跨源资源共享
uuid: e788b542-d4ac-48aa-91e2-1e88068cbba1
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 跨源资源共享 {#cross-origin-resource-sharing}

XMLHttpRequests中对withCredentials属性的支持允许跨源资源共享(CORS)请求包含针对各种请求类型的目标域的cookie。

当客户端请求清单、段或键时，服务器可以设置客户端必须为后续请求传递的cookie。 要允许读取和写入Cookie，客户端必须将跨源 `withCredentials` 请求的 `true` 属性设置为。

要在播 `withCredentials` 放给定媒体资源时支持大多数类型的请求，请执行以下操作：

1. 创建对 `CORSConfig` 象。

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. 将对 `corsConfig` 象附 `NetworkConfiguration` 加并设置 `useCookieHeaderForAllRequests` 为 `true`。

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. 在对 `networkConfig` 象中设 `MediaPlayerItemConfig` 置。

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. 传 `MediaPlayerItemConfig` 递到方 `MediaPlayer.replaceCurrentResource` 法。

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>该标 `useCookieHeaderForAllRequests` 志不影响许可证请求。 要将许可证 `withCredentials` 请求的属 `true` 性设置为，您必须在保护数据中设置该属性，或在保护数据中指 `withCredentials``httpRequestHeaders` 定授权密钥。 例如：

```
# Example 1 
{ 
    "com.widevine.alpha": {  
        "withCredentials":true,  
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i]" } 
} 
 
# Example 2 
{ 
    "com.widevine.alpha": { 
        "httpRequestHeaders": {  
            "authorization": "true"  
            }, 
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i>]" }
        } 
}
```

该标志不影响许可证请求，因为某些服务器在响应 `Access-Control-Allow-Origin` 时将字段设置为通配符(&#39;*&#39;)。 但是，当凭据标志设置为时， `true`通配符无法在中使用 `Access-Control-Allow-Origin`。 如果对所 `useCookieHeaderForAllRequests` 有类 `true` 型的请求进行设置，则可能会看到许可证请求的以下错误：

请记住以下信息：

* 当调用失败时， `withCredentials=true` 浏览器TVSDK将重试该调用，而不进行 `withCredentials`。
* 使用进行调用时， `networkConfiguration.useCookieHeaderForAllRequests=false`将发出XHR请求，而不包含该 `withCredentials` 属性。