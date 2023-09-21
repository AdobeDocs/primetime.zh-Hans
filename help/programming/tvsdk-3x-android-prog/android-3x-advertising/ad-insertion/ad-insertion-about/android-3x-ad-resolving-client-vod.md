---
description: 对于视频点播(VOD)内容，TVSDK通过在主内容中拼接广告来插入广告时间，以便增加时间轴持续时间。
title: 解析并插入VOD广告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 解析和插入VOD广告 {#resolve-and-insert-vod-ad}

对于视频点播(VOD)内容，TVSDK通过在主内容中拼接广告来插入广告时间，以便增加时间轴持续时间。

在播放之前，TVSDK会解析已知广告，并按照从Adobe Primetime ad decisioning返回的时间轴的说明，在主内容中插入广告时间，并在必要时重新计算虚拟时间轴。

TVSDK通过以下方式插入广告：

* **前置式广告**，放在内容之前。
* **中置**，位于内容中间。
* **后置式广告**，放置在内容之后。

>[!TIP]
>
>开始播放后，内容不会发生其他更改。

广告不能为：

* 已插入
* 已删除

  例如，您无法从内容中删除内置广告以提供无广告体验。
* 已替换

  例如，您不能将内置广告替换为目标广告。
