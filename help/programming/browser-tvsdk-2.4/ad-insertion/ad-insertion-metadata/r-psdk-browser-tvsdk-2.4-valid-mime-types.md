---
description: 一个广告可能有多个创意，其中一个被选中播放。
title: 有效的MIME类型
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# 有效的MIME类型{#valid-mime-types}

一个广告可能有多个创意，其中一个被选中播放。

使用MIME类型，您可以指定用户可以优先处理的创意类型。 用户指定的MIME类型和浏览器TVSDK支持的MIME类型用于确定将优先顺序排列哪些创意。

要在浏览器TVSDK中设置有效的MIME类型：

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

其中`mimeTypes`是字符串数组，每个字符串表示mime类型。

如果为广告返回多个媒体文件，则选择取决于媒体文件在`validMimeTypes`阵列中的显示顺序。 具有较低索引的MIME类型比具有较高索引的MIME类型具有首选项。
