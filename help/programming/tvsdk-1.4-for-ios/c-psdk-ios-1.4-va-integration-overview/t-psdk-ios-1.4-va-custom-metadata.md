---
description: 您可以使用回调函数为内容、广告和章节跟踪调用提供自定义元数据。
seo-description: 您可以使用回调函数为内容、广告和章节跟踪调用提供自定义元数据。
seo-title: 实现自定义元数据支持
title: 实现自定义元数据支持
uuid: eb8d383f-a3e8-402d-84e8-f4209df0f954
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# 实现自定义元数据支持{#implement-custom-metadata-support}

您可以使用回调函数为内容、广告和章节跟踪调用提供自定义元数据。

在进行跟踪调用之前调用回调函数，这样您的应用程序可以附加特定于广告或章节的元数据。

调用内容、广告和章节的回调函数。

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

