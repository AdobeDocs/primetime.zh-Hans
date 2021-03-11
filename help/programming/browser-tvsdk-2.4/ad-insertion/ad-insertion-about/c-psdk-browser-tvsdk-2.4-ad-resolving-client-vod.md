---
description: 对于视频点播(VOD)内容，Browser TVSDK通过在主内容中拼接广告来插入广告分段，从而延长时间轴持续时间。
title: VOD广告解析和插入
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# VOD广告解析和插入{#vod-ad-resolving-and-insertion}

对于视频点播(VOD)内容，Browser TVSDK通过在主内容中拼接广告来插入广告分段，从而延长时间轴持续时间。

在播放之前，Browser TVSDK会解析已知广告，按照从Adobe Primetime广告决策返回的时间轴所述在主内容中插入广告分段，并在必要时重新计算虚拟时间轴。

浏览器TVSDK以下列方式插入广告：

* **前滚**，内容之前。
* **后滚**，内容之后。

播放开始后，内容中不会发生其他更改。 广告不能：

* 已插入
* 已删除

   例如，您无法从内容中删除内置广告以优惠免费广告体验。
* 已替换

   例如，您无法将内置广告替换为目标广告。

