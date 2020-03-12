---
description: 'null'
seo-description: 'null'
seo-title: 实施章节支持
title: 实施章节支持
uuid: 70f10621-febe-4443-84e7-ce95bec53377
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 实施章节支持{#implement-chapter-support}

章节定义为每个广告中断之间的时间。 例如，预卷广告中断与第一卷中间卷之间的时间定义为第一章。 您可以使用自定义章节在基于浏览器TVSDK的应用程序中定义和跟踪视频跟踪的章节。 自定义章节由应用程序管理，并基于CMS数据或应用程序用于定义章节的其他方式。

1. 定义和跟踪自定义章节。

   ```js
   vaObj.enableChapterTracking = true; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata: 
   // For example: 3 chapters of 60 second duration each 
   var chapters = []; 
   var chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       var chapterData = new AdobePSDK.VA.VideoAnalyticsChapterData("chapter_" + (i+1), i * chapterDuration, chapterDuration, (i+1)); 
       chapters.push(chapterData); 
   } 
   
   vaObj.chapters = chapters;
   ```

