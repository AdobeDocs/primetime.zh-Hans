---
description: 对于实时流广告插入，您可能需要先退出广告时间，然后再播放广告时间中的所有广告直至结束。
title: 提前返回广告时间
exl-id: 584e870e-1408-41a9-bb6f-e82b921fe99e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# 提前返回广告时间{#implementing-an-early-ad-break-return}

对于实时流广告插入，您可能需要先退出广告时间，然后再播放广告时间中的所有广告直至结束。

>[!NOTE]
>
>您必须订阅广告插播/插入标记( `#EXT-X-CUE-OUT`， `#EXT-X-CUE-IN`、和 `#EXT-X-CUE`)。

以下是需要考虑的一些要求：

* 解析标记，例如 `EXT-X-CUE-IN` （或等效标记标签）的标记。

   将标记注册为广告提前返回点的标记。 仅播放 `adBreaks` 直到播放期间此标记位置结束，这将覆盖 `adBreak` 以行距标记 `EXE-X-CUE-OUT` 标记。

* 如果为2 `EXT-X-CUE-IN` 相同项目存在标记 `EXT-X-CUE-OUT` 标记，第一个 `EXT-X-CUE-IN` 显示的标记即为其计数标记。

* 如果 `EXE-X-CUE-IN` 标记显示在时间轴中，不带行距 `EXT-X-CUE-OUT` 标记， `EXE-X-CUE-IN` 标记将被丢弃。

   在实时流中，如果 `EXT-X-CUE-OUT` 标记器刚刚移出窗口，TVSDK不会对其进行响应。

* 当广告时间提早返回时， `adBreak` 一直播放，直到播放头恢复到广告时间本应结束的原始位置，并从该位置继续播放主内容。

## SpliceOut和SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` 和 `SpliceIn` 标记标记标记广告时间的开始和结束。 持续时间 `SpliceOut` 类型 `EXE-X-CUE` 标记可能为0，并且 `SpliceIn` 类型 `EXE-X-CUE` 标记器标记广告时间的结尾。 它们出现在一个标记中，并因类型而异。

**一个具有不同类型的标记**

例如，以下是一个具有不同类型的标记：

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

在一个具有不同类型的标记中，例如，如果 `SpliceOut` 类型为零，则 `SpliceOut` 和 `SpliceIn` 每次广告时间必须一起工作。 目前， `SpliceOut` 持续时间非零且不需要配对的标记 `SpliceIn` 标记比较典型。

**两个单独的标记**

更典型的情况是 `SpliceOut` 持续时间非零且不需要配对的标记 `SpliceIn` 标记。 这里，一个配对 `SpliceIn` 标记器在广告时间播放期间标记广告时间的结尾，但在以下位置广告时间被缩短 `SpliceIn` 标记位置，并且主内容开始在此位置播放。

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
