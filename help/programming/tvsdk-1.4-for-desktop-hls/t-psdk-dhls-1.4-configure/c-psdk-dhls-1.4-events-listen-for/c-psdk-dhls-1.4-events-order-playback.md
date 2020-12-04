---
description: TVSDK按通常预期的序列发送事件/通知。 您的播放器可以根据预期序列中的事件执行操作。
seo-description: TVSDK按通常预期的序列发送事件/通知。 您的播放器可以根据预期序列中的事件执行操作。
seo-title: 播放事件的顺序
title: 播放事件的顺序
uuid: 4a9ea66b-a383-46ff-9ab8-983b1dd7f935
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# 播放事件的顺序{#order-of-playback-events}

TVSDK按通常预期的序列发送事件/通知。 您的播放器可以根据预期序列中的事件执行操作。

<!--<a id="section_6E34A6C7936245D88DEB3315DA64598B"></a>-->

以下示例显示了包含播放事件的某些事件的顺序。

* 成功通过`MediaPlayer.replaceCurrentResource`加载媒体资源时，事件的顺序为：

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 状态  `MediaPlayerStatus.INITIALIZING`

   * `MediaPlayerItemEvent.ITEM_CREATED`
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 状态  `MediaPlayerStatus.INITIALIZED`

* 通过`MediaPlayer.prepareToPlay`准备回放时，事件的顺序为：

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 状态  `MediaPlayerStatus.PREPARING`

   * `TimelineEvent.TIMELINE_UPDATED` 是否插入广告
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 状态  `MediaPlayerStatus.PREPARED`

* 对于实时／线性流，在播放期间，随着播放窗口的前进以及其他机会的解决，事件的顺序是：

   * `MediaPlayerItemEvent.ITEM_UPDATED`
   * `TimelineEvent.TIMELINE_UPDATED` 是否插入广告

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

以下示例显示了事件的典型进度：

```
mediaPlayer.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
public function onItemCreated(event:MediaPlayerItemEvent):void { 
    var item:MediaPlayerItem = event.item; 
    ... 
} 
mediaPlayer.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
public function onItemUpdated(event:MediaPlayerItemEvent):void { 
    var item:MediaPlayerItem = event.item; 
    ... 
} 
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
public function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    switch(event.status){ 
        case MediaPlayerStatus.INITIALIZING: 
        case MediaPlayerStatus.INITIALIZED: 
        ... 
    } 
    ... 
} 
mediaPlayer.addEventListener(TimeChangeEvent.TIME_CHANGED, onTimeChanged); 
public function onTimeChanged(event:TimeChangeEvent):void { 
    var timeInMilliseconds:Number = event.time; 
    ... 
}
```

