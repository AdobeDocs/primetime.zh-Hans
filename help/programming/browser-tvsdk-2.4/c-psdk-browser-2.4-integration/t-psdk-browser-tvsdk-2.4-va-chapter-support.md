---
title: 实施章节支持
description: 实施章节支持
copied-description: true
exl-id: 8a962706-50cd-41c2-96a7-6af1b24145a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---

# 实施章节支持{#implement-chapter-support}

章节被定义为每个广告时间的间隔。 例如，前置广告时间与第一个中置广告时间之间的时间被定义为第一个章节。 您可以使用自定义章节，在基于浏览器TVSDK的应用程序中定义和跟踪视频跟踪的章节。 自定义章节由应用程序管理，并且基于CMS数据或应用程序用于定义章节的其他方式。

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
