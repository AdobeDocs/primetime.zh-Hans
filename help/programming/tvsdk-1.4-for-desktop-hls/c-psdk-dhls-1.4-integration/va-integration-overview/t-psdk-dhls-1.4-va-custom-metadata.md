---
description: 您可以使用回调函数提供关于内容、广告和章节跟踪调用的自定义元数据。
title: 实施自定义元数据支持
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# 实施自定义元数据支持{#implement-custom-metadata-support}

您可以使用回调函数提供关于内容、广告和章节跟踪调用的自定义元数据。

回调函数是在进行跟踪调用之前调用的，因此您的应用程序可以附加特定于广告或章节的元数据。

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
