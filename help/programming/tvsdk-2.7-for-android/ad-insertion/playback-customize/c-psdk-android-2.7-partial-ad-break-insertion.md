---
title: 部分广告时间插入
description: 部分广告时间插入
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 部分广告时间插入 {#partial-ad-break-insertion}

您可以实现类似电视的体验，即能够在广告中间通过直播加入。 部分广告时间功能允许您模拟类似电视的体验，如果客户端在midroll内启动实时流，它将在该midroll内启动。 它类似于切换到电视频道，广告也无缝运行。

例如，如果用户在90秒的广告时间（3个30秒的广告）的中间、第二个广告的10秒（即广告时间的40秒）内加入，则会出现以下情况：

* 第二个广告在剩余的时长（20秒）内播放，然后是第三个广告。
* 不触发部分播放的广告（第二个广告）的广告跟踪器。 仅触发第三个广告的跟踪器。

默认情况下，不启用此行为。 要在应用程序中启用此功能，请执行以下操作：

1. 使用AdvertisingMetadata类的方法setEnableLivePreroll禁用实时预滚动。

   ```
   advertisingMetadata.setLivePreroll(false)  
   advertisingMetadata.setPreroll(false)
   ```

1. 打开“部分广告时间插入”的首选项。 使用MediaPlayer接口中的新方法setPartialAdBreakPref打开此功能。 使用getPartialAdBreakPref方法查找此首选项的当前状态。

   ```
   MediaPlayer mediaPlayer = new MediaPlayer(getActivity().getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
   ```
