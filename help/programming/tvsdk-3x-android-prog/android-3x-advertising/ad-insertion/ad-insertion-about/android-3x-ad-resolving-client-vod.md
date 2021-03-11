---
description: 对于视频点播(VOD)内容，TVSDK通过在主内容中拼接广告来插入广告分段，从而延长时间线持续时间。
title: 解析和插入VOD广告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# 解析和插入VOD广告{#resolve-and-insert-vod-ad}

对于视频点播(VOD)内容，TVSDK通过在主内容中拼接广告来插入广告分段，从而延长时间线持续时间。

在播放之前，TVSDK会解析已知广告，在主内容中插入广告分段(如从Adobe Primetime广告决策返回的时间轴所描述)，并在必要时重新计算虚拟时间轴。

TVSDK通过以下方式插入广告：

* **前滚**，放在内容之前。
* **中间**，在内容中间。
* **后滚**，放在内容之后。

>[!TIP]
>
>播放开始后，内容中不会发生其他更改。

广告不能：

* 已插入
* 已删除

   例如，您无法从内容中删除内置广告以优惠免费广告体验。
* 已替换

   例如，您无法将内置广告替换为目标广告。