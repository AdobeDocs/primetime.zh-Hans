---
description: 由于某些第三方广告（或创意）的视频格式与HLS不兼容，因此无法将其拼接到HTTP实时流(HLS)内容流中。 Primetime广告插入和TVSDK可以选择性地尝试将不兼容的广告重新打包到兼容的M3U8视频中。
seo-description: 由于某些第三方广告（或创意）的视频格式与HLS不兼容，因此无法将其拼接到HTTP实时流(HLS)内容流中。 Primetime广告插入和TVSDK可以选择性地尝试将不兼容的广告重新打包到兼容的M3U8视频中。
seo-title: 使用Adobe Creative Repackaging Service(CRS)重新打包不兼容的广告
title: 使用Adobe Creative Repackaging Service(CRS)重新打包不兼容的广告
uuid: ef542d13-6d52-4429-8a1e-0af2df236f12
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 使用Adobe Creative Repackaging Service(CRS)重新打包不兼容的广告 {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

由于某些第三方广告（或创意）的视频格式与HLS不兼容，因此无法将其拼接到HTTP实时流(HLS)内容流中。 Primetime广告插入和TVSDK可以选择性地尝试将不兼容的广告重新打包到兼容的M3U8视频中。

来自不同第三方（如代理广告服务器、您的库存合作伙伴或广告网络）的广告通常以不兼容的格式提供，如渐进式下载MP4格式。

当TVSDK第一次遇到不兼容的广告时，播放器会忽略该广告并向创意重新打包服务(CRS)发出请求，以将广告重新打包为兼容格式，该服务是Primetime广告插入后端的一部分。 CRS尝试生成广告的多比特率M3U8再现，并将这些再现存储在Primetime内容交付网络(CDN)上。 下次TVSDK收到指向该广告的广告响应时，播放器将使用CDN中与HLS兼容的M3U8版本。

要激活此可选CRS功能，请与Adobe代表联系。

>[!NOTE]
>
>对于CRS 3.0版（及更早版本）客户，从CRS 3.1版开始，以下更改提高了安全性和性能：>
>* CRS 3.1在重新打包的 `https:` 内容使用时继续使用 `https:`。 这降低了某些播放器展示不安全内容的可能性。
   >
   >
* CRS 3.1极大地减少了网络调用，缩短了视频启动时间。
>



有关CRS的详细信息，请参 [阅Creative Packaging Service(CRS)](../../../../../dynamic-ad-insertion/creative-repackaging-service/crs-overview.md)。

## 在TVSDK应用程序中启用CRS {#enable-crs-in-tvsdk-applications}

要在TVSDK应用程序中启用CRS，您必须在“Auditude”设置中设置以下信息：

1. 在中启用CRS `AuditudeSettings`。

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
