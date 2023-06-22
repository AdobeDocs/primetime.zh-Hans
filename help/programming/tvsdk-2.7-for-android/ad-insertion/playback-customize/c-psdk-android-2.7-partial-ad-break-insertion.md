---
title: 部分广告时间插入
description: 部分广告时间插入
copied-description: true
exl-id: bcd4b108-9b91-479e-8147-ec4d24862e37
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 部分广告时间插入 {#partial-ad-break-insertion}

您可以启用类似电视的体验，即能够在广告中间、直播中加入。 部分广告时间功能允许您模拟类似电视的体验，如果客户端在中间轴内启动实时流，它将在该中间轴内启动。 它类似于切换到电视频道，广告也无缝运行。

例如，如果用户在90秒广告时间（3个30秒广告）的中间、第二个广告10秒（即广告时间的40秒）加入，则会发生以下情况：

* 第二个广告的播放持续了剩余的时间（20秒），随后是第三个广告。
* 不触发部分播放的广告（第二个广告）的广告跟踪器。 仅触发第三个广告的跟踪器。

默认情况下不启用此行为。 要在应用程序中启用此功能，请执行以下操作：

1. 使用AdvertisingMetadata类的方法setEnableLivePreroll禁用实时预留。

   ```
   advertisingMetadata.setLivePreroll(false)  
   advertisingMetadata.setPreroll(false)
   ```

1. 打开“部分广告时间插入”的首选项。 使用MediaPlayer界面中的新方法setPartialAdBreakPref将此功能切换为ON。 使用getPartialAdBreakPref方法查找此首选项的当前状态。

   ```
   MediaPlayer mediaPlayer = new MediaPlayer(getActivity().getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
   ```
