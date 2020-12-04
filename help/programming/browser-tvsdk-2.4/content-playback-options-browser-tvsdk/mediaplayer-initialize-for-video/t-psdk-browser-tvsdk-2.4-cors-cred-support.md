---
description: 支持XMLHttpRequests中的withCredentials属性允许跨来源资源共享(CORS)请求包含目标域的cookies以用于各种请求类型。
keywords: CORS;cross origin;resource sharing;cookies;withCredentials
seo-description: 支持XMLHttpRequests中的withCredentials属性允许跨来源资源共享(CORS)请求包含目标域的cookies以用于各种请求类型。
seo-title: 跨来源资源共享
title: 跨来源资源共享
uuid: e788b542-d4ac-48aa-91e2-1e88068cbba1
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# 跨来源资源共享{#cross-origin-resource-sharing}

支持XMLHttpRequests中的withCredentials属性允许跨来源资源共享(CORS)请求包含目标域的cookies以用于各种请求类型。

当客户端请求清单、段或密钥时，服务器可以设置客户端必须通过的cookie才能进行后续请求。 要允许读取和写入Cookie，客户端必须将跨来源请求的`withCredentials`属性设置为`true`。

要在播放给定媒体资源时启用`withCredentials`对大多数类型的请求的支持，请执行以下操作：

1. 创建`CORSConfig`对象。

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. 将`corsConfig`连接到`NetworkConfiguration`对象，并将`useCookieHeaderForAllRequests`设置为`true`。

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. 在`MediaPlayerItemConfig`对象中设置`networkConfig`。

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. 将`MediaPlayerItemConfig`传递给`MediaPlayer.replaceCurrentResource`方法。

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>`useCookieHeaderForAllRequests`标志不影响许可证请求。 要将许可证请求的`withCredentials`属性设置为`true`，必须在保护数据中设置`withCredentials`属性或在保护数据的`httpRequestHeaders`中指定授权密钥。 例如：

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

该标志不影响许可证请求，因为某些服务器在响应中将`Access-Control-Allow-Origin`字段设置为通配符(“*”)。 但是，当凭据标志设置为`true`时，通配符不能在`Access-Control-Allow-Origin`中使用。 如果将所有类型的请求的`useCookieHeaderForAllRequests`设置为`true`，则许可证请求可能会出现以下错误：

请记住以下信息：

* 当具有`withCredentials=true`的调用失败时，浏览器TVSDK将重试不具有`withCredentials`的调用。
* 使用`networkConfiguration.useCookieHeaderForAllRequests=false`进行调用时，将发出XHR请求，而不使用`withCredentials`属性。