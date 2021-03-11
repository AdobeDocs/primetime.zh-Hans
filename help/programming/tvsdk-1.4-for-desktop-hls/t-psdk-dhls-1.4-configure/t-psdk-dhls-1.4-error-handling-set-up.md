---
description: 设置一个位置来处理错误。
title: 设置错误处理
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 2%

---


# 设置错误处理{#set-up-error-handling}

设置一个位置来处理错误。

1. 为`MediaPlayerStatusChangeEvent.STATUS_CHANGED`实现事件回调函数。

   TVSDK传递事件信息，如`MediaPlayerStatusChangeEvent`对象。
1. 在回调中，当事件参数的状态为`MediaPlayerStatus.ERROR`时，请提供处理所有错误的逻辑。
1. 处理错误后，重置`MediaPlayer`对象或加载新媒体资源。

   当`MediaPlayer`对象处于ERROR状态时，在您重置`MediaPlayer`对象（通过`MediaPlayer.reset`方法）或加载新媒体资源(`MediaPlayer.replaceCurrentItem`)之前，该对象将无法退出此状态。

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

