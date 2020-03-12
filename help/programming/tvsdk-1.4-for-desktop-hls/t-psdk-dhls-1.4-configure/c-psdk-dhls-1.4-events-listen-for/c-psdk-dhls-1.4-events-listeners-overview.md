---
description: 来自TVSDK的事件指示播放器的状态、发生的错误、您请求的操作（如视频开始播放）的完成或隐式发生的操作（如广告完成）。
seo-description: 来自TVSDK的事件指示播放器的状态、发生的错误、您请求的操作（如视频开始播放）的完成或隐式发生的操作（如广告完成）。
seo-title: 聆听Primetime Player活动
title: 聆听Primetime Player活动
uuid: e72782bf-9d26-4285-85e4-fd4d803c1bbe
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# 概述 {#implement-event-listeners-and-callbacks-overview}

事件处理函数允许TVSDK对事件做出响应。 当发生事件时，TVSDK的事件机制将调用您注册的事件处理函数并将事件信息传递给该处理函数。

Flash运行时提供通用事件机制，TVSDK也使用该机制并定义一系列自定义事件。 您的应用程序必须为影响您的应用程序的TVSDK事件实施事件监听器。

有关视频分析事件的完整列表，请参阅跟 [踪核心视频播放](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_track-core-vid-playback.html)。

1. 确定应用程序必须侦听的事件。

   * **必需活动**:聆听所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件提 `MediaPlayerStatusChangeEvent.STATUS_CHANGE` 供播放器状态，包括错误。 任何状态都可能影响播放器的下一步。

   * **其他活动**:可选，具体取决于您的应用程序。

      例如，如果在播放中加入广告，请倾听所有 `AdBreakPlaybackEvent` 和事 `AdPlaybackEvent` 件。

1. 为每个事件实现事件监听器。

   TVSDK将参数值返回到事件监听器回调。 这些值提供有关事件的相关信息，您可以在监听器中使用这些事件执行相应的操作。

   该类 `Event` 列出所有回调接口。 每个接口都显示为该接口返回的参数。

   例如：

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. 使用向对象注册回调 `MediaPlayer` 监听器 `MediaPlayer.addEventListener`。

   `MediaPlayer` extends `flash.events.IEventDispatcher`，它是Flash Player核心文件的一部分，包括函数 `addEventListener` 和 `removeEventListener`。

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```


