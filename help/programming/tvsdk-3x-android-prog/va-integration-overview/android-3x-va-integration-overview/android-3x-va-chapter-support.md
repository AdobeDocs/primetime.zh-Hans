---
title: 实施章节支持
description: 实施章节支持
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---


# 实施章节支持{#implement-chapter-support}

您可以在基于TVSDK的应用程序中定义和跟踪用于视频跟踪的&#x200B;*自定义*&#x200B;章节。

自定义章节由应用程序管理，并基于CMS数据或应用程序用于定义章节的其他方式。

>[!CAUTION]
>
>3.0 Android TVSDK不支持默认章节。

定义和跟踪自定义章节。

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
