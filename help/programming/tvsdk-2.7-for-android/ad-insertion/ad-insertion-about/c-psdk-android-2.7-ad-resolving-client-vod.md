---
description: 对于视频点播(VOD)内容，TVSDK通过在主内容中拼接广告来插入广告分段，从而延长时间轴持续时间。
seo-description: 对于视频点播(VOD)内容，TVSDK通过在主内容中拼接广告来插入广告分段，从而延长时间轴持续时间。
seo-title: 解析和插入VOD广告
title: 解析和插入VOD广告
uuid: 69853c16-e252-472e-b33a-7a0e0c4b95dd
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# 解析和插入VOD广告{#resolve-and-insert-vod-ad}

对于视频点播(VOD)内容，TVSDK通过在主内容中拼接广告来插入广告分段，从而延长时间轴持续时间。

在回放之前，TVSDK会解析已知广告，按照Adobe Primetime广告决策返回的时间轴所述在主内容中插入广告中断，并在必要时重新计算虚拟时间轴。

TVSDK通过以下方式插入广告：

* **预卷**，放在内容之前。
* **中间**，在内容中间。
* **后滚**，放在内容之后。

>[!TIP]
>
>播放开始后，内容中不再发生其他更改。

广告不能是：

* 已插入
* 已删除

   例如，您不能从内容中删除内置广告以优惠免费广告体验。
* 已替换

   例如，您无法将内置广告替换为目标广告。

