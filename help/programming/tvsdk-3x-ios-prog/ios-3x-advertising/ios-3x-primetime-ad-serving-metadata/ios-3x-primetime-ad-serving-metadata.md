---
description: TVSDK支持解析和插入VOD和实时/线性流的广告。
title: Primetime广告服务器元数据
exl-id: f27657ac-4037-45e5-a658-ad9a783dd990
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 概述 {#primetime-ad-server-metadata-overview}

TVSDK支持解析和插入VOD和实时/线性流的广告。

## 先决条件

在视频内容中包含广告之前，请提供以下元数据信息：

* A `mediaID`，用于标识要播放的特定内容。
* 您的 `zoneID`，用于标识您的公司或网站。
* 广告服务器域，指定分配的广告服务器的域。
* 其他定位参数。

## 设置Primetime广告服务器元数据 {#section_86C4A3B2DF124770B9B7FD2511394313}

您的应用程序必须向TVSDK提供所需的 `PTAuditudeMetadata` 连接到广告服务器的信息。

要设置广告服务器元数据，请执行以下操作：

1. 创建实例 [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) 并设置其属性。

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. 设置 `PTAuditudeMetadata` 实例作为当前元数据 `PTMediaPlayerItem` 元数据，使用 `PTAdResolvingMetadataKey`.

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   示例如下：

   ```
   PTMetadata *metadata = [self createMetadata]; 
   PTMediaPlayerItem *item =  
     [[[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease]; 
   
   - (PTMetadata *) createMetadata { 
       PTMetadata* metadata = [[[PTMetadata alloc] init] autorelease]; 
   
       PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
       adMetadata.zoneId = yourZoneID; 
       adMetadata.domain = yourAdServerDomain; 
   
       [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   
       return metadata; 
   }
   ```
