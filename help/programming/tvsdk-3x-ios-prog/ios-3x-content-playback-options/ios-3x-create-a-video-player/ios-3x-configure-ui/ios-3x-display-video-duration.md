---
description: 您可以显示当前活动内容的持续时间。
seo-description: 您可以显示当前活动内容的持续时间。
seo-title: 显示视频的持续时间
title: 显示视频的持续时间
uuid: 945f222d-80ba-4832-a06f-9bb8db6adbcb
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 显示视频的持续时间{#display-the-duration-of-the-video}

您可以显示当前活动内容的持续时间。

使用以下示例代码实现视频持续时间显示：

    “PTMediaPlayer”属性“[seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)”包含当前可搜索窗口范围：
    
    *对于VOD，此范围是整个VOD内容范围，包括广告。
    *对于实时／线性，此范围表示可搜索窗口。
    
    有关API的详细信息，请参阅[TVSDK 3.4 for iOS API参考](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
