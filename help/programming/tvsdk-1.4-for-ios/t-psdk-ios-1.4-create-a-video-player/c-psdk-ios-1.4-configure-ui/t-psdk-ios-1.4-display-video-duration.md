---
description: 您可以显示当前活动内容的持续时间。
title: 显示视频的持续时间
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# 显示视频的持续时间{#display-the-duration-of-the-video}

您可以显示当前活动内容的持续时间。

使用以下示例代码实现视频持续时间显示：

    “PTMediaPlayer”属性[seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)包含当前可搜索窗口范围：
    
    *对于VOD，此范围是整个VOD内容范围，包括广告。
    *对于实时/线性，此范围表示可搜索窗口。
    
    有关API的详细信息，请参阅[TVSDK 1.4 for iOS API参考](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
