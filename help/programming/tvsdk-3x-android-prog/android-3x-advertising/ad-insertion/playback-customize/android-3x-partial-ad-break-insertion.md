---
description: 'null'
seo-description: 'null'
seo-title: 部分广告中断插入
title: 部分广告中断插入
uuid: a81295b8-77fe-4475-a472-080ee7804d7a
translation-type: tm+mt
source-git-commit: fe9d7d1b2b23a70eb4e212de3d9bda47fc11d8f1
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---


# 部分Ad-break插入{#partial-ad-break-insertion}

您可以在广告中间通过实时流加入，从而获得类似电视的体验。 部分广告中断功能可以模拟类似电视的体验，如果客户端开始某个媒体流内的实时内容，则该媒体流将在该媒体流内进行开始。 它类似于切换到电视渠道，广告无缝运行。

例如，如果用户在90秒的广告中断（三则30秒的广告）中间加入，在第二则广告中加入10秒（即，在广告中断开始40秒），则会发生以下情况：

* 第二个广告在剩余的持续时间（20秒）内播放，然后是第三个广告。
* 不会触发部分播放的广告（第二个广告）的广告跟踪器。 只会触发第三个广告的跟踪器。

默认情况下不启用此行为。 要在应用程序中启用此功能，请执行以下操作：

打开“部分广告中断插入”首选项。 使用MediaPlayer接口中的新方法`setPartialAdBreakPref`将此功能打开。 使用`getPartialAdBreakPref`方法查找此首选项的当前状态。

```
    MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
```

如果有预卷广告，则播放该广告，然后从实况点播放该内容，以模拟直播电视的体验。
