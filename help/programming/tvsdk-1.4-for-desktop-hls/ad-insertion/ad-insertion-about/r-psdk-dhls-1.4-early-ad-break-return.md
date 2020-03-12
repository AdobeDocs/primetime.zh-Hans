---
description: 对于实时流广告插入，您可能需要退出广告中断，然后才能播放中断中的所有广告，直到完成。
seo-description: 对于实时流广告插入，您可能需要退出广告中断，然后才能播放中断中的所有广告，直到完成。
seo-title: 实施早期广告分时段退货
title: 实施早期广告分时段退货
uuid: 984b6ed0-c929-49a3-9553-e30d1a7758ed
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 实施早期广告分时段退货{#implementing-an-early-ad-break-return}

对于实时流广告插入，您可能需要退出广告中断，然后才能播放中断中的所有广告，直到完成。

>[!NOTE] {othertype=&quot;入门项目&quot;}
>
>您必须订阅剪接／插入广告标记( `#EXT-X-CUE-OUT`、 `#EXT-X-CUE-IN`和 `#EXT-X-CUE`)。

以下是需要考虑的一些要求：

* 解析线性或FER `EXT-X-CUE-IN` 流中显示的标记，如（或等效标记标记）。

   将标记注册为广告早期返回点的标记。 在播放期 `adBreaks` 间，仅播放到此标记位置为止，这将覆盖由前导标记标 `adBreak` 记的持续时 `EXE-X-CUE-OUT` 间。

* 如果同 `EXT-X-CUE-IN` 一标记存在两个 `EXT-X-CUE-OUT` 标记，则显示的第 `EXT-X-CUE-IN` 一个标记是计数的标记。

* 如果标 `EXE-X-CUE-IN` 记显示在时间轴中，而没有前导 `EXT-X-CUE-OUT` 标记，则 `EXE-X-CUE-IN` 标记将被丢弃。

   在实时流中，如果前导标 `EXT-X-CUE-OUT` 记刚从窗口中移出，则TVSDK将不会对其做出响应。

* 当广告中断提前返回时，播放会一直播放，直到播放头返回原始位置（当广告中断应结束时），并从该位置继续播放主内容。 `adBreak`

## SpliceOut和SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` 标 `SpliceIn` 记标记广告中断的开始和结束。 标记类型的持 `SpliceOut` 续时间可 `EXE-X-CUE` 能为零，标记类型 `SpliceIn` 标记 `EXE-X-CUE` 标记广告中断的结束。 它们显示在一个标签中，并且因类型而异。

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

在具有不同类型的一个标记示例中，如果类型的持续时 `SpliceOut` 间为零，则每个广告中断 `SpliceOut` 都 `SpliceIn` 必须结合使用和。 目前， `SpliceOut` 持续时间非零且不需要配对标记的标记更 `SpliceIn` 为典型。

**两个单独的标记**

更典型的场景是持 `SpliceOut` 续时间非零的标记，不需要配对标 `SpliceIn` 记。 此处，配对标 `SpliceIn``SpliceIn` 记标记在广告中断播放期间标记广告中断的结束，但广告中断在标记位置被截断，主内容在此位置开始播放。

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

