---
description: 事件处理程序允许浏览器TVSDK响应事件。
title: 实施事件侦听器和回调
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# 实施事件侦听器和回调{#implement-event-listeners-and-callbacks}

事件处理程序允许浏览器TVSDK响应事件。

发生事件时，浏览器TVSDK的事件机制会调用已注册的事件处理程序，并将事件信息传递给处理程序。

应用程序必须为影响应用程序的浏览器TVSDK事件实施事件侦听器。

1. 确定应用程序必须侦听的事件。

   * **必需事件**：监听所有播放事件。

     >[!IMPORTANT]
     >
     >播放事件 `STATUS_CHANGED` 提供播放器状态，包括错误。 任何状态都可能影响播放器的下一步。

   * **其他事件**：可选，具体取决于您的应用程序。

     例如，如果在播放中加入广告，则监听所有 `AdBreakPlaybackEvent` 和 `AdPlaybackEvent` 事件。

1. 为每个事件实施事件侦听器。

   浏览器TVSDK会向事件侦听器回调返回参数值。 这些值提供有关事件的相关信息，您可以在监听器中使用该信息来执行相应的操作。

   例如：

   * 事件类型： `AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * 事件属性： `MediaPlayerStatus.<event>` 使用方式如下：

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

1. 在注册回调侦听器 `MediaPlayer` 对象，使用 `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
