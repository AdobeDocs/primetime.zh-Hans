---
title: 部分广告时间插入
description: 部分广告时间插入
copied-description: true
exl-id: c86f1e99-7f1e-4a1e-b285-568ad6659f45
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# 部分广告时间插入 {#partial-ad-break-insertion}

您可以启用类似电视的体验，即能够在广告中间、直播中加入。 部分广告时间功能允许您模拟类似电视的体验，如果客户端在中间轴内启动实时流，它将在该中间轴内启动。 它类似于切换到电视频道，广告也无缝运行。

例如，如果用户在90秒广告时间（3个30秒广告）的中间、第二个广告10秒（即广告时间的40秒）加入，则会发生以下情况：

* 第二个广告的播放持续了剩余的时间（20秒），随后是第三个广告。
* 不触发部分播放的广告（第二个广告）的广告跟踪器。 仅触发第三个广告的跟踪器。

默认情况下不启用此行为。 要在应用程序中启用此功能，请执行以下操作：

打开“部分广告时间插入”的首选项。 使用新方法 `setPartialAdBreakPref` 在MediaPlayer界面中打开此功能。 使用 `getPartialAdBreakPref` 方法以查找此首选项的当前状态。

```
    MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
```

播放前置广告（如果可用），然后从直播点播放内容，模拟直播电视的体验。
