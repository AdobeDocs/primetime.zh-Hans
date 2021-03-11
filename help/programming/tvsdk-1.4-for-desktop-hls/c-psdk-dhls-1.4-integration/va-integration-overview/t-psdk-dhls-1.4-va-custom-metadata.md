---
description: 您可以使用回调函数为内容、广告和章节跟踪调用提供自定义元数据。
title: 实现自定义元数据支持
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---


# 实现自定义元数据支持{#implement-custom-metadata-support}

您可以使用回调函数为内容、广告和章节跟踪调用提供自定义元数据。

在进行跟踪调用之前调用回调函数，因此应用程序可以附加特定于广告或章节的元数据。

1. 调用内容、广告和章节的回调函数。

   ```
   // Video Metadata Block 
   vaMetadata.videoMetadataBlock = function():Object { 
       return {"myvideoid":"1234", "mysdkversion":Version.version} 
   }; 
   
   // Ad Metadata Block invoked on every ad start 
   vaMetadata.adMetadataBlock = function(ad:Ad):Object { 
       return {"myadid":"ad-1234", "myad-sdkversion":Version.version} 
   }; 
   
   // Chapter Metadata Block invoked on every chapter start 
   vaMetadata.chapterMetadataBlock = function(chapter:VideoAnalyticsChapterData) { 
       return {"mychapterid":"chapter-1234", "mychapter-sdkversion":Version.version} 
   };
   ```

