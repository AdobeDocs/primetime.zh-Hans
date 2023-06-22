---
description: TVSDK调度服务质量(QoS)事件，以通知应用程序有关可能会影响QoS统计信息计算的事件，例如缓冲和搜寻事件。
title: QoS事件
exl-id: 283555cd-9ba9-45e9-a73e-76aba6993e8a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 0%

---

# QoS事件{#qos-events}

TVSDK调度服务质量(QoS)事件，以通知应用程序有关可能会影响QoS统计信息计算的事件，例如缓冲和搜寻事件。

以下示例显示了这些事件的典型过程：

```
// For buffering 
mediaPlayer.addEventListener(BufferEvent.BUFFERING_BEGIN, onBufferingBegin); 
private function onBufferingBegin(event:BufferEvent):void { ... } 
 
mediaPlayer.addEventListener(BufferEvent.BUFFERING_END, onBufferingCompleted); 
private function onBufferingCompleted(event:BufferEvent):void { ... } 
 
// For seeking 
mediaPlayer.addEventListener(SeekEvent.SEEK_BEGIN, onSeekBegin); 
private function onSeekBegin(event:SeekEvent):void { ... } 
 
mediaPlayer.addEventListener(SeekEvent.SEEK_COMPLETED, onSeekCompleted); 
private function onSeekCompleted(event:SeekEvent):void { ... } 
 
...  SeekEvent.SEEK_POSITION_ADJUSTED...  //if the desired 
// seek position is modified by the current advertising policies 
```
