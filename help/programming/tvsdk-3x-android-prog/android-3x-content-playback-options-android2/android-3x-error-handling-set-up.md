---
description: 您可以设置一个花边来处理错误。
title: 设置错误处理
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 设置错误处理 {#set-up-error-handling}

您可以设置一个花边来处理错误。

1. 为实施事件回调函数 `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK传递事件信息，如 `MediaPlayerStatusChangeEvent` 对象。
1. 在回调中，当返回的状态为 `MediaPlayerStatus.ERROR`，提供逻辑以处理所有错误。
1. 处理错误后，重置 `MediaPlayer` 对象或加载新的媒体资源。

   当 `MediaPlayer` 对象处于错误状态，除非您使用 `MediaPlayer.reset` 方法。

<!--<a id="example_E74BB605ED08450295B8902F1E4BB8F5"></a>-->

例如：

```java
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (event.getStatus() == MediaPlayerStatus.ERROR) { 
        // handle TVSDK error here 
        } 
    } 
});
```
