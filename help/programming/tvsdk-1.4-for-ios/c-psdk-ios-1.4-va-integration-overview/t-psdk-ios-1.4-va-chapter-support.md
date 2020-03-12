---
description: 'null'
seo-description: 'null'
seo-title: 实施章节支持
title: 实施章节支持
uuid: 4224cd2e-1e16-4040-972b-92c91506408f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 实施章节支持{#implement-chapter-support}

您可以通过以下方式在基于TVSDK的应用程序中定义和跟踪视频跟踪的章节：

* 默认章节，由TVSDK在内部管理。

   章节定义为每个广告中断之间的时间。 例如，预卷广告中断与第一卷中间卷之间的时间定义为第一章。
* 自定义章节，由应用程序管理，基于CMS数据或应用程序用于定义章节的其他方式。

   定义和跟踪默认或自定义章节。

   ```
   // First, enable chapter tracking by setting the boolean 'enableChapterTracking' to true: 
   
       vaTrackingMetadata.enableChapterTracking = YES; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata:  
   // For example, 3 chapters of 60 second duration each: 
   
       NSMutableArray *chapters = [[[NSMutableArray alloc] init] autorelease]; 
   
       int chapterDuration = 60; 
       for (int i = 0; i < 3; i++) 
       { 
           PTVideoAnalyticsChapterData *chapterData =  
             [[[PTVideoAnalyticsChapterData alloc] init] autorelease]; 
           chapterData.name = [NSString stringWithFormat:@"chapter_%d", (i+1)]; 
           chapterData.range =  
             CMTimeRangeMake(CMTimeMakeWithSeconds(i * chapterDuration, 10000),  
             CMTimeMakeWithSeconds(chapterDuration, 10000)); 
   
           [chapters addObject:chapterData]; 
       } 
   
       vaTrackingMetadata.chapters = chapters; 
   
   // For default chapters, the application must not set custom chapters on the tracking metadata  
   // and simply enable chapters to be tracked by setting the boolean value as defined above.
   ```

