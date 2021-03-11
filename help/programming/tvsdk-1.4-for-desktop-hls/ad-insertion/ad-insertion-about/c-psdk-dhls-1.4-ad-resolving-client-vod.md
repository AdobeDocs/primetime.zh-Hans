---
description: 对于视频点播(VOD)内容，TVSDK通过在主内容中拼接广告来插入广告分段，从而延长时间线持续时间。
title: VOD广告解析和插入
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# VOD广告解析和插入{#vod-ad-resolving-and-insertion}

对于视频点播(VOD)内容，TVSDK通过在主内容中拼接广告来插入广告分段，从而延长时间线持续时间。

在播放之前，TVSDK会解析已知广告，在TVSDK返回的时间轴所描述的主内容中插入广告中断，并在必要时重新计算虚拟时间轴。

TVSDK通过以下方式插入广告：

* **前滚**，内容之前。
* **中间版**，内容中。
* **后滚**，内容之后。

>[!IMPORTANT]
>
>在实施自定义`AdPolicySelector`时，可以根据`AdBreakTimelineItem`的类型，为`AdPolicyInfo`中的每种类型`AdBreakTimelineItem`（前滚、中滚或后滚）提供不同的策略。 例如，您可以在播放中间卷内容后保留该内容，但在播放后删除前置卷内容。

播放开始后，内容中不会发生其他更改。 广告不能：

* 已插入
* 已删除

   例如，您无法从内容中删除内置广告以优惠免费广告体验。
* 已替换

   例如，您无法将内置广告替换为目标广告。

