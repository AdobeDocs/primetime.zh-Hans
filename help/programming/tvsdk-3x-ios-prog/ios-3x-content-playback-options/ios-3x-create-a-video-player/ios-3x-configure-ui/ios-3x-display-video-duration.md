---
description: 您可以显示当前活动内容的持续时间。
title: 显示视频的持续时间
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# 显示视频的持续时间 {#display-the-duration-of-the-video}

您可以显示当前活动内容的持续时间。

使用以下示例代码实施视频持续时间显示：

此 `PTMediaPlayer` 属性， [seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)，包含当前可搜索窗口范围：

* 对于VOD，此范围是整个VOD内容范围，包括广告。
* 对于实时/线性，此范围表示可搜索窗口。

有关API的更多信息，请参阅 [适用于iOS API的TVSDK 3.4参考](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
