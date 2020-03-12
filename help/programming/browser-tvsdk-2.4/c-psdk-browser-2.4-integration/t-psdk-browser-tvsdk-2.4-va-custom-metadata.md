---
description: 您可以使用回调函数为内容、广告和章节跟踪调用提供自定义元数据。
seo-description: 您可以使用回调函数为内容、广告和章节跟踪调用提供自定义元数据。
seo-title: 实施自定义元数据支持
title: 实施自定义元数据支持
uuid: 6e23311c-a393-4485-919e-4cf6412789b1
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 实施自定义元数据支持{#implement-custom-metadata-support}

您可以使用回调函数为内容、广告和章节跟踪调用提供自定义元数据。

回调函数在进行跟踪调用之前即被调用，因此您的应用程序可以附加特定于广告或章节的元数据。

1. 调用内容、广告和章节的回调函数。

   ```js
   vaObj.videoMetadataBlock = function() { 
       return { 
           "name" : "my-video", 
           "genre" : "comedy" 
       }; 
   } 
   
   vaObj.adMetadataBlock = function(ad) { 
       return { 
           "name" : "my-ad", 
           "category" : "automotive" 
       }; 
   } 
   
   vaObj.chapterMetadataBlock = function(chapter) { 
       return { 
           "name" : "my-chapter", 
           "type" : "quartile" 
       }; 
   }
   ```

