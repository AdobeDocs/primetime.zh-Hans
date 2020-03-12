---
description: 设置一个位置以处理错误。
seo-description: 设置一个位置以处理错误。
seo-title: 设置错误处理
title: 设置错误处理
uuid: ff56180d-aa74-4b7c-a24c-e536d874c2e6
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 设置错误处理{#set-up-error-handling}

设置一个位置以处理错误。

1. 为实现事件回调函数 `MediaPlayerStatusChangeEvent.STATUS_CHANGED`。

   TVSDK传递事件信息，如对 `MediaPlayerStatusChangeEvent` 象。
1. 在回调中，当事件参数的状态为时，提供 `MediaPlayerStatus.ERROR`处理所有错误的逻辑。
1. 处理错误后，重置对 `MediaPlayer` 象或加载新媒体资源。

   当对 `MediaPlayer` 象处于ERROR状态时，只有重置对象（通过方法）或加载新媒体资源( `MediaPlayer``MediaPlayer.reset``MediaPlayer.replaceCurrentItem`)后，该对象才能退出此状态。

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

