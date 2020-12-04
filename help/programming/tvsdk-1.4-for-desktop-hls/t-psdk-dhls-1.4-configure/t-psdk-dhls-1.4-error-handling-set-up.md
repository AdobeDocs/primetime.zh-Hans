---
description: 设置一个位置来处理错误。
seo-description: 设置一个位置来处理错误。
seo-title: 设置错误处理
title: 设置错误处理
uuid: ff56180d-aa74-4b7c-a24c-e536d874c2e6
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 1%

---


# 设置错误处理{#set-up-error-handling}

设置一个位置来处理错误。

1. 为`MediaPlayerStatusChangeEvent.STATUS_CHANGED`实现事件回调函数。

   TVSDK传递事件信息，如`MediaPlayerStatusChangeEvent`对象。
1. 在回调中，当事件参数的状态为`MediaPlayerStatus.ERROR`时，请提供处理所有错误的逻辑。
1. 处理错误后，重置`MediaPlayer`对象或加载新媒体资源。

   当`MediaPlayer`对象处于ERROR状态时，只有重置`MediaPlayer`对象（通过`MediaPlayer.reset`方法）或加载新媒体资源(`MediaPlayer.replaceCurrentItem`)后，该对象才能退出此状态。

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

