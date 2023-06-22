---
title: 配套横幅广告的最佳实践
description: 配套横幅广告的最佳实践
copied-description: true
exl-id: e7d15916-9059-4993-a588-baf7d7ddc534
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# 配套横幅广告的最佳实践 {#best-practices-for-companion-banner-ads}

TVSDK支持随附横幅广告，这些广告是线性广告伴随的广告，通常在线性广告结束后保留在页面上。 您的应用程序负责显示随线性广告一起提供的随附横幅。

显示伴随广告时，请遵循以下建议：

* 尝试在播放器的布局中尽可能多地展示视频广告的伴随横幅广告。
* 仅当您的位置与广告的指定高度和宽度相匹配时，才会显示随附横幅。

   >[!IMPORTANT]
   >
   >请勿调整广告大小。

* 在广告开始后尽快开始展示伴随横幅。
* 不要用随附横幅覆盖主广告/视频容器。
* 您可以在广告结束后显示随附横幅。

标准做法是显示每个随附横幅，直到您有广告的替代项为止。
