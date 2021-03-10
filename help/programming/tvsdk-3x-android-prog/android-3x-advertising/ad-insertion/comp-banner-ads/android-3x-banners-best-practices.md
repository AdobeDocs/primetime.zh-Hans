---
title: 伴侣横幅广告的最佳实践
description: 伴侣横幅广告的最佳实践
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---


# 伴侣横幅广告{#best-practices-for-companion-banner-ads}的最佳实践

TVSDK支持伴侣横幅广告，这些广告是线性广告附带的广告，在线性广告结束后通常保留在页面上。 您的应用程序负责显示随线性广告提供的附属横幅。

显示配套广告时，请遵循以下建议：

* 尝试展示视频广告的配套横幅广告中的任意多个，以适合您播放器的布局。
* 仅当您的位置与广告的指定高度和宽度匹配时，才显示配套横幅。

   >[!IMPORTANT]
   >
   >不要调整广告大小。

* 在广告开始后尽快开始展示配套横幅。
* 请勿将主广告/视频容器与附带横幅叠加。
* 您可以在广告结束后显示配套横幅。

标准做法是在您有广告替代品之前显示每个附带横幅。