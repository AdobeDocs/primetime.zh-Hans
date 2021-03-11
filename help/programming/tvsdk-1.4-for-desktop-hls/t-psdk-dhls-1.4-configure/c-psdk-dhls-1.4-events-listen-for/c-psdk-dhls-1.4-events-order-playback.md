---
description: TVSDK按通常预期的序列调度事件/通知。 您的播放器可以根据预期序列中的事件来实施操作。
title: 播放事件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# 播放事件的顺序{#order-of-playback-events}

TVSDK按通常预期的序列调度事件/通知。 您的播放器可以根据预期序列中的事件来实施操作。

<!--<a id="section_6E34A6C7936245D88DEB3315DA64598B"></a>-->

以下示例显示了包含播放事件的某些事件的顺序。

* 通过`MediaPlayer.replaceCurrentResource`成功加载媒体资源时，事件的顺序为：

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 状态  `MediaPlayerStatus.INITIALIZING`

   * `MediaPlayerItemEvent.ITEM_CREATED`
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 状态  `MediaPlayerStatus.INITIALIZED`

* 当通过`MediaPlayer.prepareToPlay`准备播放时，事件的顺序为：

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 状态  `MediaPlayerStatus.PREPARING`

   * `TimelineEvent.TIMELINE_UPDATED` 是否插入了广告
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 状态  `MediaPlayerStatus.PREPARED`

* 对于实时/线性流，在播放过程中，随着播放窗口的前进和其他机会的解决，事件的顺序是：

   * `MediaPlayerItemEvent.ITEM_UPDATED`
   * `TimelineEvent.TIMELINE_UPDATED` 是否插入了广告

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

以下示例显示了典型的事件进度：

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

