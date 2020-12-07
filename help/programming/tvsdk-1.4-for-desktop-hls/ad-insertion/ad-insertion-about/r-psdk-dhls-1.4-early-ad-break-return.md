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


# 实施早期广告中断返回{#implementing-an-early-ad-break-return}

对于实时流广告插入，您可能需要退出广告分段，然后才能播放分段中的所有广告完成。

>[!NOTE]
>
>必须订阅剪接／插入广告标记（`#EXT-X-CUE-OUT`、`#EXT-X-CUE-IN`和`#EXT-X-CUE`）。

以下是需要考虑的一些要求：

* 解析线性或FER流中显示的标记，如`EXT-X-CUE-IN`（或等效标记标记）。

   将标记注册为广告早期返回点的标记。 在播放期间，仅播放`adBreaks`，直到此标记位置为止，该位置会覆盖由前导`EXE-X-CUE-OUT`标记标记的`adBreak`的持续时间。

* 如果同一`EXT-X-CUE-OUT`标记存在两个`EXT-X-CUE-IN`标记，则显示的第一个`EXT-X-CUE-IN`标记是计数的标记。

* 如果时间轴中显示`EXE-X-CUE-IN`标记，且没有前导`EXT-X-CUE-OUT`标记，则放弃`EXE-X-CUE-IN`标记。

   在实时流中，如果前导`EXT-X-CUE-OUT`标记刚从窗口移出，TVSDK将不响应它。

* 当广告中断提前返回时，`adBreak`将播放，直到播放头返回原始位置（当广告中断应结束时），并从该位置继续播放主内容。

## SpliceOut和SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` 标 `SpliceIn` 记标记广告片段的开始和结束。`EXE-X-CUE`标记的`SpliceOut`类型的持续时间可能为零，而`SpliceIn`类型的`EXE-X-CUE`标记标记标记广告中断的结束。 它们显示在一个标签中，并因类型而异。

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

在具有不同类型的一个标记示例中，如果`SpliceOut`类型的持续时间为零，则`SpliceOut`和`SpliceIn`必须共同处理每个广告中断。 目前，持续时间为非零的`SpliceOut`标记更为典型，不需要配对`SpliceIn`标记。

**两个单独的标记**

更典型的情形是持续时间非零的`SpliceOut`标记，不需要配对`SpliceIn`标记。 此处，配对`SpliceIn`标记标记标记在广告中断播放期间标记广告中断的结束，但广告中断在`SpliceIn`标记位置被截断，主内容开始在此位置播放。

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

