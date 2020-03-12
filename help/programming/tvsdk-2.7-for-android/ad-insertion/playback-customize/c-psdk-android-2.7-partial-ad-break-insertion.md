---
description: 'null'
seo-description: 'null'
seo-title: 部分广告中断插入
title: 部分广告中断插入
uuid: cc071c89-f813-419e-a2b2-4f6a9fdccd6a
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 部分广告中断插入 {#partial-ad-break-insertion}

您可以在广告中间、在直播流中加入，从而获得类似电视的体验。 通过部分广告中断功能，您可以模拟类似电视的体验，如果客户端在midroll中启动实时流，它将在该midroll中启动。 它类似于切换到电视频道，广告无缝运行。

例如，如果用户在90秒广告中断（3个30秒广告）中间加入，在第2个广告中加入10秒（即，在广告中断后40秒），则会发生以下情况：

* 在剩余持续时间（20秒）内播放第二个广告，然后播放第三个广告。
* 不触发部分播放广告（第二个广告）的广告跟踪器。 只触发第三个广告的跟踪器。

默认情况下不启用此行为。 要在应用程序中启用此功能，请执行以下操作：

1. 使用AdvertisingMetadata类的方法setEnableLivePreroll禁用实时预卷。

   ```
   advertisingMetadata.setLivePreroll(false)  
   advertisingMetadata.setPreroll(false)
   ```

1. 打开“部分插入广告中断”首选项。 使用MediaPlayer界面中的新方法setPartialAdBreakPref打开此功能。 使用getPartialAdBreakPref方法查找此首选项的当前状态。

   ```
   MediaPlayer mediaPlayer = new MediaPlayer(getActivity().getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
   ```

