---
description: PlayerFragment类是编辑代码以创建完全启用的功能管理器的位置。
seo-description: PlayerFragment类是编辑代码以创建完全启用的功能管理器的位置。
seo-title: PlayerFragment
title: PlayerFragment
uuid: 83f02c31-f3b1-4d16-97c8-5b391e8c999a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# PlayerFragment {#playerfragment}

PlayerFragment类是编辑代码以创建完全启用的功能管理器的位置。

类 `PlayerFragment` 包含所有UI组件， `playerFrame`如 `ControlBar`、 `playerClickableAdFragment`和 `adOverlay`。

它处理所有这些组件的初始化以及创建播放器、设置视图、为媒体播放器创建功能管理器、处理媒体事件（如恢复、播放和暂停）以及处理事件监听器( `QoSManager`、、、、 `DRMManager`、 `CCManager``AAManager`和) `AdsManager``PlaybackManager``EntitlementManager`。

包含配置参数的XML文 `PlayerFragment` 件是 `res/layout/fragment_player.xml`。

在创建功能管理器之前，您需要通过确保文件中包含以下代码来创建媒体播 `PlayerFragment.java` 放器：

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
