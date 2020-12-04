---
description: 'null'
seo-description: 'null'
seo-title: 实施章节支持
title: 实施章节支持
uuid: 85d14b83-7910-4f5d-9ef2-511de916abd6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# 实施章节支持{#implement-chapter-support}

您可以通过以下方式在基于TVSDK的应用程序中定义和跟踪视频跟踪的章节：

* 默认章节，由TVSDK在内部管理。

   章节定义为每个广告时段之间的时间。 例如，预卷广告中断与第一中间卷之间的时间被定义为第一章。
* 自定义章节，由应用程序管理，基于CMS数据或应用程序用于定义章节的其他方式。

   定义和跟踪默认或自定义章节。

   ```
   // First, enable chapter tracking by setting the boolean 'enableChapterTracking' to true: 
   
       vaMetadata.enableChapterTracking = true; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata:  
   // For example: 3 chapters of 60 second duration each 
   
       var chapters:Vector.<VideoAnalyticsChapterData> = new Vector.<VideoAnalyticsChapterData>(); 
       var chapterDuration:int = 60; 
       for (var i:int = 0; i < 3; i++) { 
           var chapterData:VideoAnalyticsChapterData =  
             new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration); 
           chapterData.name = "chapter_%d" + (i+1); 
   
           chapters.push(chapterData); 
       } 
   
       vaMetadata.chapters = chapters; 
   
   // For default chapters, the application must not set custom chapters on the tracking metadata  
   // and simply enable chapters to be tracked by setting the boolean value as defined above. 
   ```

