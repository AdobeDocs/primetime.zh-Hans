---
description: 对于视频点播(VOD)内容，TVSDK通过在主内容中拼接广告来插入广告时间，以便增加时间轴持续时间。
title: VOD广告解析和插入
exl-id: 2e45fc35-85ca-4e34-b300-cf65878eeac6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# VOD广告解析和插入{#vod-ad-resolving-and-insertion}

对于视频点播(VOD)内容，TVSDK通过在主内容中拼接广告来插入广告时间，以便增加时间轴持续时间。

在播放之前，TVSDK会解析已知广告，并按照从Adobe Primetime ad decisioning返回的时间线中的说明，在主内容中插入广告时间，并在必要时重新计算虚拟时间线。

TVSDK通过以下方式插入广告：

* **前置式广告**，在内容之前。
* **中置**，即位于内容中。
* **后置广告**，在内容之后。

开始播放后，内容不会发生其他更改。 广告不能为：

* 已插入
* 已删除

   例如，您无法从内容中删除内置广告以提供无广告体验。
* 已替换

   例如，您不能将内置广告替换为目标广告。
