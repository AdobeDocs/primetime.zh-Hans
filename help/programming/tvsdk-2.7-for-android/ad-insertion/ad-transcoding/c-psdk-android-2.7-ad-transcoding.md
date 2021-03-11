---
description: 无法将某些第三方广告（或创意）拼接到HTTP实时流(HLS)内容流中，因为其视频格式与HLS不兼容。 Primetime广告插入和TVSDK可以选择尝试将不兼容的广告重新打包到兼容的M3U8视频中。
title: 使用Adobe Creative Repackaging Service(CRS)重新打包不兼容的广告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# 使用Adobe Creative Repackaging Service(CRS){#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}重新打包不兼容的广告

无法将某些第三方广告（或创意）拼接到HTTP实时流(HLS)内容流中，因为其视频格式与HLS不兼容。 Primetime广告插入和TVSDK可以选择尝试将不兼容的广告重新打包到兼容的M3U8视频中。

来自不同第三方（如代理广告服务器、您的库存合作伙伴或广告网络）的广告通常以不兼容的格式提供，如渐进式下载MP4格式。

当TVSDK第一次遇到不兼容的广告时，播放器会忽略该广告并向创意重新打包服务(CRS)发出请求，以将广告重新打包为兼容格式，该服务是Primetime广告插入后端的一部分。 CRS尝试生成广告的多位速率M3U8再现，并将这些再现存储在Primetime内容投放网络(CDN)上。 下次TVSDK收到指向该广告的广告响应时，播放器将使用CDN中与HLS兼容的M3U8版本。

要激活此可选CRS功能，请与Adobe代表联系。

>[!NOTE]
>
>对于CRS 3.0版（及更早版本）客户，从CRS 3.1版开始，以下更改提高了安全性和性能：
>
>* 如果重新打包的内容使用`https:`，则CRS 3.1将继续`https:`。 这降低了某些播放器呈现不安全内容的可能性。
   >
   >
* CRS 3.1大大减少了网络调用，缩短了视频启动时间。

>



有关CRS的详细信息，请参阅[创意包装服务(CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_certificate_enrollment.pdf)。

## 在TVSDK应用程序中启用CRS{#enable-crs-in-tvsdk-applications}

要在TVSDK应用程序中启用CRS，必须在Auditude设置中设置以下信息：

1. 在`AuditudeSettings`中启用CRS。

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
