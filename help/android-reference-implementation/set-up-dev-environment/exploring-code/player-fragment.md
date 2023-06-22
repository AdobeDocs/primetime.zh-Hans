---
description: 在PlayerFragment类中，您可以编辑代码以创建完全启用的功能管理器。
title: 播放器片段
exl-id: 9060f0f5-9148-48cd-b89b-718607dd70bc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# 播放器片段 {#playerfragment}

在PlayerFragment类中，您可以编辑代码以创建完全启用的功能管理器。

此 `PlayerFragment` 类包含所有UI组件，例如 `playerFrame`， `ControlBar`， `playerClickableAdFragment`、和 `adOverlay`.

它处理所有这些组件的初始化，以及创建播放器、设置视图、为媒体播放器创建功能管理器、处理恢复、播放和暂停等媒体事件，并处理事件侦听器 `QoSManager`， `DRMManager`， `CCManager`， `AAManager`， `AdsManager`， `PlaybackManager`、和 `EntitlementManager`.

包含配置参数的XML文件 `PlayerFragment` 是 `res/layout/fragment_player.xml`.

在创建功能管理器之前，您需要通过确保以下代码位于 `PlayerFragment.java` 文件：

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
