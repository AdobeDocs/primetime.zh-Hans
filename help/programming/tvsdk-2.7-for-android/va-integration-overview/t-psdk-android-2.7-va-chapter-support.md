---
description: 'null'
seo-description: 'null'
seo-title: 实施章节支持
title: 实施章节支持
uuid: f62a8244-6393-4a38-9ae2-8ac31f6a8a06
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 实施章节支持 {#implement-chapter-support}

您可以在基于TVSDK的应 *用程序中* ，为视频跟踪定义和跟踪自定义章节。

自定义章节由应用程序管理，并基于CMS数据或应用程序用于定义章节的其他方式。

>[!CAUTION]
>
>2.5 Android TVSDK不支持默认章节。

1. 定义和跟踪自定义章节。

   ```java
   // First, enable chapter tracking by setting   
   // enableChapterTracking to true: 
   
   vaMetadata.enableChapterTracking(true); 
   // For custom chapter definitions, provide  
   // an array list of chapters through the metadata. 
   // For example: 3 chapters of 60 second duration each 
   
   List<VideoAnalyticsChapterData> chapters =  
     new ArrayList<VideoAnalyticsChapterData>(); 
   
   Int chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       VideoAnalyticsChapterData chapterData =  
         new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration);  
       chapterData.setName("chapter_" + (i+1)); 
       chapters.add(chapterData); 
   } 
   
   vaMetadata.setChapters(chapters); 
   ```

