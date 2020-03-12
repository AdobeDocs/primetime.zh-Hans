---
description: 您可以在应用程序中设置一个位置以执行错误处理以响应错误状态。
seo-description: 您可以在应用程序中设置一个位置以执行错误处理以响应错误状态。
seo-title: 设置错误处理
title: 设置错误处理
uuid: 9e650ea7-86cb-4489-a3fd-80cd2ccef41f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 设置错误处理{#set-up-error-handling}

您可以在应用程序中设置一个位置以执行错误处理以响应错误状态。

1. 为添加事件监听器 `AdobePSDK.MediaPlayerStatusChangeEvent`。

   例如：

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. 在事件监听器中，如果是， `event.status` 请提 `AdobePSDK.MediaPlayerStatus.ERROR`供处理所有错误的逻辑。
1. 处理错误后，重置对 `MediaPlayer` 象或加载新媒体资源。

       当MediaPlayer对象处于“错误”状态时，在您完成以下任务之一之前，它无法退出此状态：
   
   * 使用方法重置MediaPlayer对 `MediaPlayer.reset` 象。
   * 使用该方法加载新媒体 `MediaPlayer.replaceCurrentResource` 资源。

<!--<a id="example_342CA5A8CD7C45BD88233C5BDBB17220"></a>-->

例如：

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange); 
onStatusChange = function (event) { 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.ERROR: 
            //handle error 
            break; 
    } 
} 
```

