---
description: 来自TVSDK的事件指示播放器的状态、发生的错误、您请求的操作（如视频开始播放）的完成情况，或隐式发生的操作（如广告结束）。
title: 监听Primetime播放器事件
exl-id: 3a740245-a9e1-4e36-8761-f9f4b4e85b93
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 概述 {#implement-event-listeners-and-callbacks-overview}

事件处理程序允许TVSDK响应事件。 发生事件时，TVSDK的事件机制会调用您注册的事件处理程序，并将事件信息传递给处理程序。

Flash运行时提供了一个通用事件机制，TVSDK也使用该机制并定义了一系列自定义事件。 您的应用程序必须为影响您的应用程序的TVSDK事件实施事件侦听器。

1. 确定应用程序必须侦听哪些事件。

   * **必需事件**:监听所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件`MediaPlayerStatusChangeEvent.STATUS_CHANGE`提供播放器状态，包括错误。 任何状态都可能会影响播放器的下一步。

   * **其他事件**:可选，具体取决于您的应用程序。

      例如，如果在播放中包含广告，请监听所有`AdBreakPlaybackEvent`和`AdPlaybackEvent`事件。

1. 为每个事件实施事件侦听器。

   TVSDK会将参数值返回到事件侦听器回调中。 这些值提供有关事件的相关信息，以便您在监听器中执行适当的操作。

   `Event`类列出所有回调接口。 每个界面都显示为该界面返回的参数。

   例如：

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. 使用`MediaPlayer.addEventListener`在`MediaPlayer`对象中注册回调侦听器。

   `MediaPlayer` 扩展， `flash.events.IEventDispatcher`这是Flash播放器核心文件的一部分，包含函 `addEventListener` 数和 `removeEventListener`。

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```
