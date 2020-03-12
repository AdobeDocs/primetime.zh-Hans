---
description: 您可以设置一个花边来处理错误。
seo-description: 您可以设置一个花边来处理错误。
seo-title: 设置错误处理
title: 设置错误处理
uuid: fde47fa5-5ca5-4be5-a7e7-3227c5e4c670
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# 设置错误处理 {#set-up-error-handling}

您可以设置一个花边来处理错误。

1. 为实现事件回调函数 `MediaPlayerEvent.STATUS_CHANGED`。

   TVSDK传递事件信息，如对 `MediaPlayerStatusChangeEvent` 象。
1. 在回调中，当返回的状态为时， `MediaPlayerStatus.ERROR`提供处理所有错误的逻辑。
1. 处理错误后，重置对 `MediaPlayer` 象或加载新媒体资源。

   当对 `MediaPlayer` 象处于错误状态时，它将保持该状态，直到您使用方法重置它 `MediaPlayer.reset` 为止。

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

