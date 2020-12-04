---
description: 'null'
seo-description: 'null'
seo-title: 实施章节支持
title: 实施章节支持
uuid: 6e2c3994-d28b-489f-ae60-9b876125a871
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# 实施章节支持{#implement-chapter-support}

您可以定义和跟踪&#x200B;*自定义*&#x200B;章节，以便在基于TVSDK的应用程序中进行视频跟踪。

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
