---
description: 您可以使用回调函数提供有关内容、广告和章节跟踪调用的自定义元数据。
title: 实施自定义元数据支持
exl-id: d5d8b476-0f7c-434c-9386-d060a6eb99f9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# 实施自定义元数据支持 {#implement-custom-metadata-support}

您可以使用回调函数提供有关内容、广告和章节跟踪调用的自定义元数据。

回调函数会在进行跟踪调用之前调用，因此您的应用程序可以附加特定于广告或章节的元数据。

1. 为内容、广告和章节调用回调函数。

   ```
   // Video Metadata Block 
       vaTrackingMetadata.videoMetadataBlock = ^NSDictionary *() 
       { 
           return @{ 
                    @"myvideoid": @"1234", 
                    @"mysdkversion": [PTSDK apiVersion] 
                    }; 
       }; 
   
   // Ad Metadata Block invoked on every ad start 
       vaTrackingMetadata.adMetadataBlock = ^NSDictionary *(PTAd *ad) 
       { 
           return @{ 
                    @"myadid": @"ad-1234", 
                    @"myad-sdkversion": [PTSDK apiVersion] 
                    }; 
       }; 
   
   // Chapter Metadata Block invoked on every chapter start 
       vaTrackingMetadata.chapterMetadataBlock = ^NSDictionary *(PTVideoAnalyticsChapterData *chapter) 
       { 
           return @{ 
                    @"mychapterid": @"chapter-1234", 
                    @"mychapter-sdkversion": [PTSDK apiVersion] 
                    }; 
       };
   ```
