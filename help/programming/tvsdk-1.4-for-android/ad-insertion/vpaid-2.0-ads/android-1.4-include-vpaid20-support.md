---
description: 要添加VPAID 2.0支持，请添加自定义广告视图和适当的侦听器。
title: 实施VPAID 2.0集成
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# 实施VPAID 2.0集成{#implement-vpaid-integration}

要添加VPAID 2.0支持，请添加自定义广告视图和适当的侦听器。

要添加VPAID 2.0支持，请执行以下操作：

1. 将自定义广告视图添加到播放器界面。

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. 为自定义广告事件添加侦听器。

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

