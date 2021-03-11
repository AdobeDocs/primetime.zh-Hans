---
title: 部分广告分段插入
description: 部分广告分段插入
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# 部分Ad-break插入{#partial-ad-break-insertion}

您可以在广告中间加入直播流，从而获得类似电视的体验。 部分广告中断功能可让您模拟类似电视的体验，如果客户端开始某个视频流内部，则该视频流将在该视频中开始。 它类似于切换到电视渠道，广告无缝运行。

例如，如果用户在90秒广告时段（3个30秒广告）中间加入，在第2个广告时段（即广告时段40秒）中加入10秒，则会发生以下情况：

* 第二个广告在剩余的持续时间（20秒）内播放，然后是第三个广告。
* 不触发部分播放的广告（第二个广告）的广告跟踪器。 只触发第三个广告的跟踪器。

默认情况下不启用此行为。 要在应用程序中启用此功能，请执行以下操作：

打开“部分插入广告中断”首选项。 使用MediaPlayer接口中的新方法`setPartialAdBreakPref`将此功能打开。 使用`getPartialAdBreakPref`方法查找此首选项的当前状态。

```
    MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
```

如果有，将播放前置广告，然后内容从实时点播放，模仿直播电视的体验。
