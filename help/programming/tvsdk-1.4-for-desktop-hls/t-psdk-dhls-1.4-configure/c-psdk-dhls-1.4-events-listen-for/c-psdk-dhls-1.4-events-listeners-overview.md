---
description: 来自TVSDK的事件指示播放器的状态、发生的错误、您请求的操作（如视频开始播放）的完成，或隐式发生的操作（如广告完成）。
seo-description: 来自TVSDK的事件指示播放器的状态、发生的错误、您请求的操作（如视频开始播放）的完成，或隐式发生的操作（如广告完成）。
seo-title: 聆听Primetime Player事件
title: 聆听Primetime Player事件
uuid: e72782bf-9d26-4285-85e4-fd4d803c1bbe
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# 概述{#implement-event-listeners-and-callbacks-overview}

事件处理函数允许TVSDK对事件做出响应。 发生事件时，TVSDK的事件机制将调用注册的事件处理程序，并将事件信息传递给该处理程序。

Flash运行时提供通用事件机制，TVSDK也使用该机制并定义一系列自定义事件。 您的应用程序必须为影响您的应用程序的TVSDK事件事件实施监听器。

有关视频分析事件的完整列表，请参阅[跟踪核心视频播放](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_track-core-vid-playback.html)。

1. 确定您的应用程序必须监听哪些事件。

   * **必需事件**:聆听所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件`MediaPlayerStatusChangeEvent.STATUS_CHANGE`提供播放器状态，包括错误。 任何状态都可能影响玩家的下一步。

   * **其他事件**:可选，具体取决于您的应用程序。

      例如，如果在播放中加入广告，请倾听所有`AdBreakPlaybackEvent`和`AdPlaybackEvent`事件。

1. 为每个事件实施事件监听器。

   TVSDK将参数值返回给事件监听器回调。 这些值提供有关事件的相关信息，您可以在监听器中使用这些信息来执行适当的操作。

   `Event`类列表所有回调接口。 每个接口都显示为该接口返回的参数。

   例如：

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. 使用`MediaPlayer.addEventListener`向`MediaPlayer`对象注册回调监听器。

   `MediaPlayer` 扩展 `flash.events.IEventDispatcher`，它是Flash播放器核心文件的一部分，并包含这些 `addEventListener` 函数 `removeEventListener`和

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```


