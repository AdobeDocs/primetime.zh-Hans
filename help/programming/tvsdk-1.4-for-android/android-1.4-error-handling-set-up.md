---
description: 设置单个位置以处理错误。
title: 设置错误处理
exl-id: 2d0e0d08-d932-4b6e-8f95-494a2e666827
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# 设置错误处理{#set-up-error-handling}

设置单个位置以处理错误。

1. 为实施事件回调函数 `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK传递事件信息，例如 `MediaPlayerStatusChangeEvent` 对象。
1. 在回调中，当返回的状态为 `MediaPlayerState.ERROR`，提供逻辑以处理所有错误。
1. 处理错误后，重置 `MediaPlayer` 对象或加载新媒体资源。

   当 `MediaPlayer` 对象处于错误状态，除非您使用 `MediaPlayer.reset` 方法。

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

例如：

```java
mediaPlayer.addEventListener( 
  MediaPlayerEvent.STATUS_CHANGED, new StatusChangedEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (event.getStatus() == MediaPlayerStatus.ERROR) { 
            // handle TVSDK error here 
        } 
    } 
});
```
