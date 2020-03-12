---
description: 'null'
seo-description: 'null'
seo-title: 伴侣横幅广告的最佳实践
title: 伴侣横幅广告的最佳实践
uuid: 0e4c98cd-5e16-4c84-848f-02bc6f1b0d6e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 伴侣横幅广告的最佳实践 {#best-practices-for-companion-banner-ads}

TVSDK支持伴侣横幅广告，这些广告是线性广告附带的广告，通常在线性广告结束后保留在页面上。 您的应用程序负责显示随线性广告提供的配套横幅。

显示配套广告时，请遵循以下建议：

* 尝试展示视频广告的配套横幅广告的数量与播放器布局中的相同。
* 仅当您的位置与广告的指定高度和宽度匹配时，才显示配套横幅。

   >[!IMPORTANT]
   >
   >请勿调整广告大小。

* 在广告开始后，立即开始展示配套横幅。
* 请勿将主广告／视频容器与配套横幅叠加。
* 您可以在广告结束后显示配套横幅。

标准做法是显示每个配套横幅，直到您更换了广告。