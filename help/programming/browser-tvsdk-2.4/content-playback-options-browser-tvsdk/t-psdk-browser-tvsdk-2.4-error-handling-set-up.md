---
description: 您可以在应用程序中设置一个位置，以响应ERROR状态执行错误处理。
title: 设置错误处理
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 设置错误处理{#set-up-error-handling}

您可以在应用程序中设置一个位置，以响应ERROR状态执行错误处理。

1. 添加事件侦听器 `AdobePSDK.MediaPlayerStatusChangeEvent`.

   例如：

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. 在事件侦听器中，当 `event.status` 是 `AdobePSDK.MediaPlayerStatus.ERROR`，提供逻辑以处理所有错误。
1. 处理错误后，重置 `MediaPlayer` 对象或加载新的媒体资源。

       当MediaPlayer对象处于ERROR状态时，在完成以下任务之一之前，它无法退出此状态：
   
   * 使用重置MediaPlayer对象 `MediaPlayer.reset` 方法。
   * 使用加载新的媒体资源 `MediaPlayer.replaceCurrentResource` 方法。

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
