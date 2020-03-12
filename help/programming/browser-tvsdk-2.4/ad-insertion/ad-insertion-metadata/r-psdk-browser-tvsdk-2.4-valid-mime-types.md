---
description: 广告可能具有多个创意，其中一个被选择播放。
seo-description: 广告可能具有多个创意，其中一个被选择播放。
seo-title: 有效的MIME类型
title: 有效的MIME类型
uuid: ab2baac9-a9ef-44f1-83a1-2e6e471e3231
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 有效的MIME类型{#valid-mime-types}

广告可能具有多个创意，其中一个被选择播放。

使用MIME类型，您可以指定用户可以优先处理的创意类型。 用户指定的MIME类型和浏览器TVSDK支持的MIME类型用于确定将按优先顺序排列哪些创意。

要在浏览器TVSDK中设置有效的mime类型，请执行以下操作：

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

其中 `mimeTypes` 是字符串的数组，每个字符串表示mime类型。

如果为广告返回多个媒体文件，则选择取决于媒体文件在数组中的显示顺 `validMimeTypes` 序。 具有较低索引的MIME类型比具有较高索引的MIME类型更优先。
