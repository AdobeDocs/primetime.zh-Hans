---
description: 某些第三方广告（或创意）无法拼合到HTTP实时流(HLS)内容流中，因为其视频格式与HLS不兼容。 Primetime广告插入和TVSDK可以选择尝试将不兼容的广告重新打包到兼容的M3U8视频中。
title: 使用AdobeCreative Repackaging Service (CRS)重新打包不兼容的广告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# 使用AdobeCreative Repackaging Service (CRS)重新打包不兼容的广告 {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

某些第三方广告（或创意）无法拼合到HTTP实时流(HLS)内容流中，因为其视频格式与HLS不兼容。 Primetime广告插入和TVSDK可以选择尝试将不兼容的广告重新打包到兼容的M3U8视频中。

由不同第三方提供的广告，例如代理广告服务器、库存合作伙伴或广告网络，通常以不兼容的格式投放，例如渐进式下载MP4格式。

当TVSDK首次遇到不兼容的广告时，播放器会忽略该广告并向创意重新打包服务(CRS)（Primetime广告插入后端的一部分）发出请求，以将广告重新打包为兼容格式。 CRS会尝试生成广告的多比特率M3U8演绎版，并将这些演绎版存储在Primetime内容交付网络(CDN)上。 下次TVSDK收到指向该广告的广告响应时，播放器将使用来自CDN的HLS兼容M3U8版本。

要激活此可选CRS功能，请联系您的Adobe代表。

>[!NOTE]
>
>对于CRS版本3.0（及更早版本）客户，从CRS版本3.1开始，以下更改提高了安全性和性能：
>
>* CRS 3.1继续使用 `https:` 如果重新打包的内容使用 `https:`. 这降低了某些播放器展示不安全内容的可能性。
>
>* CRS 3.1可极大地减少网络调用，从而缩短视频启动时间。
>

## 在TVSDK应用程序中启用CRS {#enable-crs-in-tvsdk-applications}

要在TVSDK应用程序中启用CRS，必须在Auditude设置中设置以下信息：

1. 在中启用CRS `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
