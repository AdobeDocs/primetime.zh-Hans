---
description: 您可以使用回调函数为内容、广告和章节跟踪调用提供自定义元数据。
seo-description: 您可以使用回调函数为内容、广告和章节跟踪调用提供自定义元数据。
seo-title: 实施自定义元数据支持
title: 实施自定义元数据支持
uuid: 2186db58-10b0-43a6-840f-53ab289843ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 实施自定义元数据支持{#implement-custom-metadata-support}

您可以使用回调函数为内容、广告和章节跟踪调用提供自定义元数据。

回调函数在进行跟踪调用之前即被调用，因此您的应用程序可以附加特定于广告或章节的元数据。

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

