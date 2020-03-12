---
description: 对于视频点播(VOD)内容，浏览器TVSDK通过在主内容中拼接广告来插入广告分段，从而延长时间线持续时间。
seo-description: 对于视频点播(VOD)内容，浏览器TVSDK通过在主内容中拼接广告来插入广告分段，从而延长时间线持续时间。
seo-title: VOD广告解析和插入
title: VOD广告解析和插入
uuid: 34a30ae5-d553-4c5d-9829-8e5eaa41c104
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# VOD广告解析和插入{#vod-ad-resolving-and-insertion}

对于视频点播(VOD)内容，浏览器TVSDK通过在主内容中拼接广告来插入广告分段，从而延长时间线持续时间。

在播放之前，浏览器TVSDK会解析已知广告，按照Adobe Primetime广告决策返回的时间轴所述在主内容中插入广告分段，并在必要时重新计算虚拟时间轴。

浏览器TVSDK通过以下方式插入广告：

* **预卷**，内容之前。
* **后滚动**，内容之后。

播放开始后，内容中不会发生其他更改。 广告不能是：

* 已插入
* 已删除

   例如，您不能从内容中删除内置广告以提供免广告体验。
* 已更换

   例如，您不能将内置广告替换为目标广告。

