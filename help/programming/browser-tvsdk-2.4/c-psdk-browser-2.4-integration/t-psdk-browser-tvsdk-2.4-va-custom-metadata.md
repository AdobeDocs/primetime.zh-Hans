---
description: 您可以使用回调函数提供有关内容、广告和章节跟踪调用的自定义元数据。
title: 实施自定义元数据支持
exl-id: d2291649-79e2-4935-8980-4f2038d58342
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# 实施自定义元数据支持{#implement-custom-metadata-support}

您可以使用回调函数提供有关内容、广告和章节跟踪调用的自定义元数据。

回调函数会在进行跟踪调用之前调用，因此您的应用程序可以附加特定于广告或章节的元数据。

1. 为内容、广告和章节调用回调函数。

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
