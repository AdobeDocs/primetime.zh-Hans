---
description: 设置一个位置来处理错误。
seo-description: 设置一个位置来处理错误。
seo-title: 设置错误处理
title: 设置错误处理
uuid: a3182fce-85ac-4dad-bdb3-f9bfbdb2c62d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 2%

---


# 设置错误处理{#set-up-error-handling}

设置一个位置来处理错误。

1. 为`MediaPlayerEvent.STATUS_CHANGED`实现事件回调函数。

   TVSDK传递事件信息，如`MediaPlayerStatusChangeEvent`对象。
1. 在回调中，当返回的状态为`MediaPlayerState.ERROR`时，提供处理所有错误的逻辑。
1. 处理错误后，重置`MediaPlayer`对象或加载新媒体资源。

   当`MediaPlayer`对象处于错误状态时，它将保持该状态，直到您使用`MediaPlayer.reset`方法重置它。

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

