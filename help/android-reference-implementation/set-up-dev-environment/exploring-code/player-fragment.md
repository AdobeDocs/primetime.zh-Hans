---
description: PlayerFragment类是您编辑代码以创建完全启用的功能管理器的位置。
seo-description: PlayerFragment类是您编辑代码以创建完全启用的功能管理器的位置。
seo-title: PlayerFragment
title: PlayerFragment
uuid: 83f02c31-f3b1-4d16-97c8-5b391e8c999a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# PlayerFragment {#playerfragment}

PlayerFragment类是您编辑代码以创建完全启用的功能管理器的位置。

`PlayerFragment`类包含所有UI组件，如`playerFrame`、`ControlBar`、`playerClickableAdFragment`和`adOverlay`。

它处理所有这些组件的初始化以及创建播放器、设置视图、为媒体播放器创建功能管理器、处理恢复、播放和暂停等媒体事件，并处理`QoSManager`、`DRMManager`、`CCManager`、`AAManager`、`AdsManager`、`PlaybackManager`和`EntitlementManager`的事件监听器。

包含`PlayerFragment`配置参数的XML文件为`res/layout/fragment_player.xml`。

在创建功能管理器之前，您需要通过确保`PlayerFragment.java`文件中包含以下代码来创建媒体播放器：

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
