---
description: TVSDK中的事件可指示播放器的状态、发生的错误、请求的操作（如视频开始播放）的完成或隐式发生的操作（如广告完成）。
title: 监听Primetime播放器事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 概述 {#implement-event-listeners-and-callbacks-overview}

事件处理程序允许TVSDK响应事件。 发生事件时，TVSDK的事件机制会调用已注册的事件处理程序，并将事件信息传递给处理程序。

Flash运行时提供了一般事件机制，TVSDK也使用该机制并定义了一系列自定义事件。 应用程序必须为影响应用程序的TVSDK事件实施事件侦听器。

1. 确定应用程序必须侦听的事件。

   * **必需事件**：监听所有播放事件。

     >[!IMPORTANT]
     >
     >播放事件 `MediaPlayerStatusChangeEvent.STATUS_CHANGE` 提供播放器状态，包括错误。 任何状态都可能影响播放器的下一步。

   * **其他事件**：可选，具体取决于您的应用程序。

     例如，如果在播放中加入广告，则监听所有 `AdBreakPlaybackEvent` 和 `AdPlaybackEvent` 事件。

1. 为每个事件实施事件侦听器。

   TVSDK会向事件侦听器回调返回参数值。 这些值提供有关事件的相关信息，您可以在监听器中使用该信息来执行相应的操作。

   此 `Event` 类列出了所有回调接口。 每个接口都会显示为该接口返回的参数。

   例如：

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. 在注册回调侦听器 `MediaPlayer` 对象，使用 `MediaPlayer.addEventListener`.

   `MediaPlayer` 扩展 `flash.events.IEventDispatcher`，是Flash播放器核心文件的一部分，包含各种功能 `addEventListener` 和 `removeEventListener`.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```
