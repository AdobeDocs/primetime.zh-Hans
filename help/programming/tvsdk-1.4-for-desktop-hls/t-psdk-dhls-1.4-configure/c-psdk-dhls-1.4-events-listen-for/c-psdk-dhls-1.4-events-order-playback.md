---
description: TVSDK按通常预期的序列调度事件/通知。 您的播放器可以按照预期顺序基于事件实施操作。
title: 播放事件的顺序
exl-id: d03692f6-04b9-4962-92d1-fad671d06665
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 播放事件的顺序{#order-of-playback-events}

TVSDK按通常预期的序列调度事件/通知。 您的播放器可以按照预期顺序基于事件实施操作。

<!--<a id="section_6E34A6C7936245D88DEB3315DA64598B"></a>-->

以下示例显示了一些包括播放事件的事件的顺序。

* 通过成功加载媒体资源时 `MediaPlayer.replaceCurrentResource`，事件的顺序为：

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 状态 `MediaPlayerStatus.INITIALIZING`

   * `MediaPlayerItemEvent.ITEM_CREATED`
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 状态 `MediaPlayerStatus.INITIALIZED`

* 通过准备播放时 `MediaPlayer.prepareToPlay`，事件的顺序为：

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 状态 `MediaPlayerStatus.PREPARING`

   * `TimelineEvent.TIMELINE_UPDATED` 如果插入了广告
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 状态 `MediaPlayerStatus.PREPARED`

* 对于实时/线性流，在播放期间，当播放窗口前进并解决其他机会时，事件的顺序为：

   * `MediaPlayerItemEvent.ITEM_UPDATED`
   * `TimelineEvent.TIMELINE_UPDATED` 如果插入了广告

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

以下示例显示了事件的典型进展：

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
