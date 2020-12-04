---
description: 对于视频点播(VOD)内容，TVSDK通过在主内容中拼接广告来插入广告分段，从而延长时间轴持续时间。
seo-description: 对于视频点播(VOD)内容，TVSDK通过在主内容中拼接广告来插入广告分段，从而延长时间轴持续时间。
seo-title: VOD广告解析和插入
title: VOD广告解析和插入
uuid: 33280792-ad08-41c1-b180-cc2159e8137c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# VOD广告解析和插入{#vod-ad-resolving-and-insertion}

对于视频点播(VOD)内容，TVSDK通过在主内容中拼接广告来插入广告分段，从而延长时间轴持续时间。

在回放之前，TVSDK会解析已知广告，按照Adobe Primetime广告决策返回的时间轴所述在主内容中插入广告中断，并在必要时重新计算虚拟时间轴。

TVSDK通过以下方式插入广告：

* **预卷**，内容之前。
* **中间卷**，内容中。
* **后滚动**，在内容之后。

播放开始后，内容中不再发生其他更改。 广告不能是：

* 已插入
* 已删除

   例如，您不能从内容中删除内置广告以优惠免费广告体验。
* 已替换

   例如，您无法将内置广告替换为目标广告。

