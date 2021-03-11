---
description: 您可以设置一个位置来处理错误。
title: 设置错误处理
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 2%

---


# 设置错误处理{#set-up-error-handling}

您可以设置一个位置来处理错误。

1. 为`MediaPlayerEvent.STATUS_CHANGED`实现事件回调函数。

   TVSDK传递事件信息，如`MediaPlayerStatusChangeEvent`对象。
1. 在回调中，当返回的状态为`MediaPlayerStatus.ERROR`时，请提供处理所有错误的逻辑。
1. 处理错误后，重置`MediaPlayer`对象或加载新媒体资源。

   当`MediaPlayer`对象处于错误状态时，它将保持该状态，直到您使用`MediaPlayer.reset`方法重置它。

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
