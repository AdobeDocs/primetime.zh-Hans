---
title: 实施章节支持
description: 实施章节支持
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 实施章节支持 {#implement-chapter-support}

您可以通过以下方式，在基于TVSDK的应用程序中定义和跟踪视频跟踪的章节：

* 默认章节，由TVSDK内部管理。

  章节被定义为每个广告时间的间隔。 例如，前置广告时间与第一个中置广告时间之间的时间定义为第一章。
* 自定义章节，这些章节由应用程序管理，并基于CMS数据或应用程序用于定义章节的其他方式。

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
