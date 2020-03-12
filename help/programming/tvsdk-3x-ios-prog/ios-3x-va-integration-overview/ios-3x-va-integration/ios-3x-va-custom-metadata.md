---
description: 您可以使用回调函数为内容、广告和章节跟踪调用提供自定义元数据。
seo-description: 您可以使用回调函数为内容、广告和章节跟踪调用提供自定义元数据。
seo-title: 实施自定义元数据支持
title: 实施自定义元数据支持
uuid: 229681f5-ff77-4321-8022-b8ccf2928fb3
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 实施自定义元数据支持 {#implement-custom-metadata-support}

您可以使用回调函数为内容、广告和章节跟踪调用提供自定义元数据。

回调函数在进行跟踪调用之前即被调用，因此您的应用程序可以附加特定于广告或章节的元数据。

1. 调用内容、广告和章节的回调函数。

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
