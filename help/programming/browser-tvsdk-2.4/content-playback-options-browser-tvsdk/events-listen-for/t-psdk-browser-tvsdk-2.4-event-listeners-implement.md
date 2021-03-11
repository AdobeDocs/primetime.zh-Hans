---
description: 事件处理函数允许浏览器TVSDK对事件做出响应。
title: 实现事件监听器和回呼
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---


# 实现事件监听器和回调{#implement-event-listeners-and-callbacks}

事件处理函数允许浏览器TVSDK对事件做出响应。

发生事件时，浏览器TVSDK的事件机制将调用注册的事件处理程序，并将事件信息传递给该处理程序。

您的应用程序必须为影响您的应用程序的浏览器TVSDK事件实施事件侦听器。

1. 确定您的应用程序必须侦听哪些事件。

   * **必需事件**:聆听所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件`STATUS_CHANGED`提供播放器状态，包括错误。 任何状态都可能影响玩家的下一步。

   * **其他事件**:可选，具体取决于您的应用程序。

      例如，如果在播放中加入广告，请侦听所有`AdBreakPlaybackEvent`和`AdPlaybackEvent`事件。

1. 为每个事件实现事件侦听器。

   浏览器TVSDK会将参数值返回给您的事件侦听器回调。 这些值提供有关可在监听器中用于执行适当操作的事件的相关信息。

   例如：

   * 事件类型:`AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * 事件属性：`MediaPlayerStatus.<event>`使用如下：

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

1. 使用`MediaPlayer.addEventListener`向`MediaPlayer`对象注册回调侦听器。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
