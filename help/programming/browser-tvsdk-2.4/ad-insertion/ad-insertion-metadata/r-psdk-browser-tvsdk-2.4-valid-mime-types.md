---
description: 一个广告可能具有多个创意内容，其中有一个创意内容被选择播放。
title: 有效的MIME类型
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# 有效的MIME类型{#valid-mime-types}

一个广告可能具有多个创意内容，其中有一个创意内容被选择播放。

对于MIME类型，您可以指定用户可以优先处理哪些创意类型。 用户指定的mime类型以及浏览器TVSDK支持的mime类型用于确定将优先处理哪些创意。

要在浏览器TVSDK中设置有效的MIME类型，请执行以下操作：

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

位置 `mimeTypes` 是一个字符串数组，每个字符串表示一个mime类型。

如果为广告返回了多个媒体文件，则选择取决于媒体文件在中出现的顺序 `validMimeTypes` 数组。 低索引的mime类型比高索引的mime类型优先。
