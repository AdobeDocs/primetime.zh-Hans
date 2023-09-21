---
description: 在PlayerFragment类中，您可以编辑代码以创建完全启用的功能管理器。
title: Playerfragment
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Playerfragment {#playerfragment}

在PlayerFragment类中，您可以编辑代码以创建完全启用的功能管理器。

此 `PlayerFragment` 类包含所有UI组件，例如 `playerFrame`， `ControlBar`， `playerClickableAdFragment`、和 `adOverlay`.

它处理所有这些组件的初始化，以及创建播放器、设置视图、为媒体播放器创建功能管理器、处理诸如恢复、播放和暂停等媒体事件和处理事件侦听器 `QoSManager`， `DRMManager`， `CCManager`， `AAManager`， `AdsManager`， `PlaybackManager`、和 `EntitlementManager`.

包含配置参数的XML文件 `PlayerFragment` 是 `res/layout/fragment_player.xml`.

在创建功能管理器之前，您需要通过确保以下代码位于 `PlayerFragment.java` 文件：

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
