---
description: 要添加VPAID 2.0支持，请添加自定义广告视图和相应的监听器。
seo-description: 要添加VPAID 2.0支持，请添加自定义广告视图和相应的监听器。
seo-title: 实施VPAID 2.0集成
title: 实施VPAID 2.0集成
uuid: 7d11ffd8-240c-4a95-94e6-ff4417c8942e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 实施VPAID 2.0集成{#implement-vpaid-integration}

要添加VPAID 2.0支持，请添加自定义广告视图和相应的监听器。

要添加VPAID 2.0支持，请执行以下操作：

1. 将自定义广告视图添加到播放器界面。

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. 为自定义广告事件添加监听器。

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

