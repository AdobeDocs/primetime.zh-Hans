---
description: 设置单个位置以处理错误。
title: 设置错误处理
exl-id: ce4a2954-0166-43af-afdf-0aa24659f1ae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# 设置错误处理{#set-up-error-handling}

设置单个位置以处理错误。

1. 为实施事件回调函数 `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   TVSDK传递事件信息，例如 `MediaPlayerStatusChangeEvent` 对象。
1. 在回调中，当事件参数的状态为 `MediaPlayerStatus.ERROR`，提供逻辑以处理所有错误。
1. 处理错误后，重置 `MediaPlayer` 对象或加载新媒体资源。

   当 `MediaPlayer` 对象处于ERROR状态，除非重置 `MediaPlayer` 对象(通过 `MediaPlayer.reset` 方法)或加载新媒体资源( `MediaPlayer.replaceCurrentItem`)。

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

例如：

```
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
 
private void onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    if (event.status == MediaPlayerStatus.ERROR) { 
        var error:MediaError = event.error; 
        // handle TVSDK error here 
    } 
} 
```
