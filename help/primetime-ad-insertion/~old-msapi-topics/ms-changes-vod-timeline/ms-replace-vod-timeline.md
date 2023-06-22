---
description: 适合一个VOD内容播放的广告时间线可能不适合后续播放。 您可以替换VOD时间线而不更改内容。
title: 对VOD的更改
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# 对VOD的更改 {#changes-to-vod}

适合一个VOD内容播放的广告时间线可能不适合后续播放。 您可以替换VOD时间线而不更改内容。

您可能希望替换VOD时间线的情形包括：

* 替换本地广告，但在C3时段内保留国家广告。
* 在C3窗口关闭后，替换烧录广告。
* 使用持续时间较长的较新广告动态替换旧的C3广告。
* 插入较少的广告或完全不插入广告。

您可以通过提交新的广告插入请求来替换广告时间线，该请求具有原始M3U8文件，并且其 `pttimeline` 查询参数。