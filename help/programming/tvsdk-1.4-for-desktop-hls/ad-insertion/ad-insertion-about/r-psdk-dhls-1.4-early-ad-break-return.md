---
description: 对于实时流广告插入，您可能需要退出广告分段，然后才能播放分段中的所有广告完成。
seo-description: 对于实时流广告插入，您可能需要退出广告分段，然后才能播放分段中的所有广告完成。
seo-title: 实施早期广告中断退回
title: 实施早期广告中断退回
uuid: 984b6ed0-c929-49a3-9553-e30d1a7758ed
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# 实施早期广告中断退回{#implementing-an-early-ad-break-return}

对于实时流广告插入，您可能需要退出广告分段，然后才能播放分段中的所有广告完成。

>[!NOTE]
>
>必须订阅剪接／插入广告标记( `#EXT-X-CUE-OUT`、 `#EXT-X-CUE-IN`和 `#EXT-X-CUE`)。

以下是需要考虑的一些要求：

* 解析线性或 `EXT-X-CUE-IN` FER流中显示的标记（或等效标记标记）。

   将标记注册为广告早期返回点的标记。 在播放 `adBreaks` 过程中，仅播放到此标记位置，这将覆盖由前导标记 `adBreak` 标记的持续 `EXE-X-CUE-OUT` 时间。

* 如果同 `EXT-X-CUE-IN` 一标记存在 `EXT-X-CUE-OUT` 两个标记，则显 `EXT-X-CUE-IN` 示的第一个标记是计数的标记。

* 如果标 `EXE-X-CUE-IN` 记显示在时间轴中，而没有前 `EXT-X-CUE-OUT` 导标记，则 `EXE-X-CUE-IN` 将放弃标记。

   在实时流中，如果前导标 `EXT-X-CUE-OUT` 记刚从窗口中移出，TVSDK将不会对其做出响应。

* 当广告中断提前返回时，播放 `adBreak` 将一直播放到播放头返回原始位置，此时广告中断应结束并重新开始从该位置播放主内容。

## SpliceOut和SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` 标 `SpliceIn` 记标记广告片段的开始和结束。 标记类型的 `SpliceOut` 持续时 `EXE-X-CUE` 间可能为零，标记 `SpliceIn` 类型 `EXE-X-CUE` 标记标记广告中断的结束。 它们显示在一个标签中，并因类型而异。

**一个具有不同类型的标记**

例如，下面是一个具有不同类型的标记：

```
#EXTM3U#EXT-X-TARGETDURATION:10
#EXT-X-VERSION:3
#EXT-X-MEDIA-SEQUENCE:44
  
#EXTINF:9.9,
https://server-host/path/file44.ts
#EXTINF:4.2,
https://server-host/path/file45.ts
  
#EXT-X-CUE:TYPE="SpliceOut",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138",AVAIL-NUM="1",AVAILS-EXPECTED="10"
#EXTINF:5.8,
https://server-host/path/file46.ts
#EXTINF:9.9,
https://server-host/path/file47.ts
...
#EXTINF:9.9,
https://server-host/path/file56.ts
#EXTINF:4.2,
https://server-host/path/file57.ts
#EXT-X-CUE:TYPE="SpliceIn",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138"
#EXTINF:9.9,
https://server-host/path/file58.ts
```

在具有不同类型的一个标记示例中，如果类型的持 `SpliceOut` 续时间为零，则 `SpliceOut` 和 `SpliceIn` 必须在每个广告中断时协同工作。 目前， `SpliceOut` 持续时间为非零且不需要配对标记的标记更 `SpliceIn` 为典型。

**两个单独的标记**

更典型的情景是 `SpliceOut` 具有非零持续时间的标记，它不需要配对标 `SpliceIn` 记。 在此，配对标 `SpliceIn` 记标记在播放广告中断期间标记广告中断的结束，但广告中断在标记位置被截断， `SpliceIn` 主内容开始在此位置播放。

例如，下面是两个单独的标记：

```
#EXT-X-CUE-OUT:ID=105,DURATION=30.0,TIME=1081.08
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589090425811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589150485811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589210545811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589270605811,format=m3u8-aapl-v4)
#EXT-X-CUE-IN:ID=105,TIME=1105.104
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589330665811,format=m3u8-aapl-v4)
```

