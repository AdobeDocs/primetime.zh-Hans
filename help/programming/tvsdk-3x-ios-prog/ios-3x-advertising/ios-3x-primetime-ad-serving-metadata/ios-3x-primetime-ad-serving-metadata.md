---
description: TVSDK支持解析和插入用于VOD和实时／线性流的广告。
seo-description: TVSDK支持解析和插入用于VOD和实时／线性流的广告。
seo-title: Primetime广告服务器元数据
title: Primetime广告服务器元数据
uuid: 61e224dd-551a-438f-8560-e64915087fef
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 概述 {#primetime-ad-server-metadata-overview}

TVSDK支持解析和插入用于VOD和实时／线性流的广告。

[!PREREQUISITE] {othertype=&quot;Preseit&quot;}

在视频内容中包含广告之前，请提供以下元数据信息：

* A `mediaID`，它标识要播放的特定内容。
* 您的 `zoneID`公司或网站，它标识您的公司或网站。
* 您的广告服务器域，它指定您分配的广告服务器的域。
* 其他定位参数。

## 设置Primetime广告服务器元数据 {#section_86C4A3B2DF124770B9B7FD2511394313}

应用程序必须向TVSDK提供连接到广 `PTAuditudeMetadata` 告服务器所需的信息。

设置广告服务器元数据：

1. 创建PTAuditudeMetadata的 [实例](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) ，并设置其属性。

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. 通过使用 `PTAuditudeMetadata` 将实例设置为当前元数据 `PTMediaPlayerItem` 的元数据 `PTAdResolvingMetadataKey`。

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   以下是一个示例：

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
