---
description: XMLHttpRequests中对withCredentials属性的支持允许跨源资源共享(CORS)请求包含各种请求类型的目标域的Cookie。
keywords: CORS；跨域；资源共享；Cookie；withCredentials
title: 跨源资源共享
exl-id: 02826c87-b0c6-495b-a17d-67c5693a9772
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 跨源资源共享 {#cross-origin-resource-sharing}

XMLHttpRequests中对withCredentials属性的支持允许跨源资源共享(CORS)请求包含各种请求类型的目标域的Cookie。

当客户端请求清单、区段或密钥时，服务器可能会设置客户端必须为后续请求传递的Cookie。 要允许读取和写入Cookie，客户端必须将 `withCredentials` 属性至 `true` 用于跨域请求。

启用 `withCredentials` 在播放给定媒体资源时，支持大多数类型的请求：

1. 创建 `CORSConfig` 对象。

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. 附加 `corsConfig` 到 `NetworkConfiguration` 对象和集 `useCookieHeaderForAllRequests` 到 `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. 设置 `networkConfig` 在 `MediaPlayerItemConfig` 对象。

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. 通过 `MediaPlayerItemConfig` 到 `MediaPlayer.replaceCurrentResource` 方法。

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>此 `useCookieHeaderForAllRequests` 标记不会影响许可证请求。 要设置 `withCredentials` 属性至 `true` 对于许可证请求，您必须设置 `withCredentials` 属性访问，或在 `httpRequestHeaders` 保护数据的ID。 例如：

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

该标记不会影响许可证请求，因为某些服务器将 `Access-Control-Allow-Origin` 字段到通配符(&#39;&#42;&#39;)的响应中。 但是，当凭据标记设置为 `true`，通配符不能用于 `Access-Control-Allow-Origin`. 如果您设置 `useCookieHeaderForAllRequests` 到 `true` 对于所有类型的请求，您可能会看到许可证请求的以下错误：

请记住以下信息：

* 调用时 `withCredentials=true` 失败，浏览器TVSDK重试调用，但不执行 `withCredentials`.
* 调用时 `networkConfiguration.useCookieHeaderForAllRequests=false`，XHR请求不使用 `withCredentials` 属性。
