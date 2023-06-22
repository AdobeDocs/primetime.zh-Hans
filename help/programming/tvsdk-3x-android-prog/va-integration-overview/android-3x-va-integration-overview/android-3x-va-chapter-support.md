---
title: 实施章节支持
description: 实施章节支持
copied-description: true
exl-id: 2db335b3-1d9b-4339-b1b6-e12ee0f06566
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# 实施章节支持 {#implement-chapter-support}

您可以定义和跟踪 *自定义* 有关基于TVSDK的应用程序中视频跟踪的章节。

自定义章节由应用程序管理，并且基于CMS数据或应用程序用于定义章节的其他方式。

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
