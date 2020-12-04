---
description: 事件处理程序允许浏览器TVSDK对事件做出响应。
seo-description: 事件处理程序允许浏览器TVSDK对事件做出响应。
seo-title: 实现事件监听器和回呼
title: 实现事件监听器和回呼
uuid: 63f62c60-505e-4f83-bc0d-58895d85a75a
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 1%

---


# 实现事件监听器和回调{#implement-event-listeners-and-callbacks}

事件处理程序允许浏览器TVSDK对事件做出响应。

发生事件时，浏览器TVSDK的事件机制将调用注册的事件处理程序，并将事件信息传递给该处理程序。

您的应用程序必须为影响您的应用程序的浏览器TVSDK事件事件实施监听器。

1. 确定您的应用程序必须监听哪些事件。

   * **必需事件**:聆听所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件`STATUS_CHANGED`提供播放器状态，包括错误。 任何状态都可能影响玩家的下一步。

   * **其他事件**:可选，具体取决于您的应用程序。

      例如，如果在播放中加入广告，请倾听所有`AdBreakPlaybackEvent`和`AdPlaybackEvent`事件。

1. 为每个事件实施事件监听器。

   浏览器TVSDK会将参数值返回给事件监听器回调。 这些值提供有关事件的相关信息，您可以在监听器中使用这些信息来执行适当的操作。

   例如：

   * 事件类型:`AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * 事件属性：`MediaPlayerStatus.<event>`用途如下：

```js
player.addEventListener( 
            AdobePSDK.PSDKEventType.STATUS_CHANGED,  
            onStatusChange); 
 
onStatusChange = function (event) { 
 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.IDLE: 
            console.log("Player Status: IDLE"); 
            break;
```

1. 使用`MediaPlayer.addEventListener`向`MediaPlayer`对象注册回调监听器。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
