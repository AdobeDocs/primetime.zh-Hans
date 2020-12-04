---
description: 您可以在应用程序中设置一个位置以执行错误处理以响应ERROR状态。
seo-description: 您可以在应用程序中设置一个位置以执行错误处理以响应ERROR状态。
seo-title: 设置错误处理
title: 设置错误处理
uuid: 9e650ea7-86cb-4489-a3fd-80cd2ccef41f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 2%

---


# 设置错误处理{#set-up-error-handling}

您可以在应用程序中设置一个位置以执行错误处理以响应ERROR状态。

1. 为`AdobePSDK.MediaPlayerStatusChangeEvent`添加事件监听器。

   例如：

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. 在事件监听器中，当`event.status`为`AdobePSDK.MediaPlayerStatus.ERROR`时，请提供处理所有错误的逻辑。
1. 处理错误后，重置`MediaPlayer`对象或加载新媒体资源。

       当MediaPlayer对象处于ERROR状态时，在您完成以下任一任务后，它将无法退出此状态：
   
   * 使用`MediaPlayer.reset`方法重置MediaPlayer对象。
   * 使用`MediaPlayer.replaceCurrentResource`方法加载新媒体资源。

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

