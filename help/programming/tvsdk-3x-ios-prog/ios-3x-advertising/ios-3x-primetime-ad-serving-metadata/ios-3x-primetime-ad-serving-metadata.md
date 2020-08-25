---
description: TVSDK支持解析和插入用于VOD和实时／线性流的广告。
seo-description: TVSDK支持解析和插入用于VOD和实时／线性流的广告。
seo-title: Primetime广告服务器元数据
title: Primetime广告服务器元数据
uuid: 61e224dd-551a-438f-8560-e64915087fef
translation-type: tm+mt
source-git-commit: 9d60bff4035963572e49fa49effa576ca854f799
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# 概述 {#primetime-ad-server-metadata-overview}

TVSDK支持解析和插入用于VOD和实时／线性流的广告。

## 入门项目

在视频内容中包含广告之前，请提供以下元数据信息：

* A, `mediaID`它标识要播放的特定内容。
* 您的 `zoneID`，它标识您的公司或网站。
* 广告服务器域，它指定所分配广告服务器的域。
* 其他定位参数。

## 设置Primetime广告服务器元数据 {#section_86C4A3B2DF124770B9B7FD2511394313}

您的应用程序必须向TVSDK提 `PTAuditudeMetadata` 供连接到广告服务器所需的信息。

设置广告服务器元数据：

1. 创建PTAuditudeMetadata [实例](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) ，并设置其属性。

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. 使用将 `PTAuditudeMetadata` 实例设置为当前元数据 `PTMediaPlayerItem` 的元数据 `PTAdResolvingMetadataKey`。

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
