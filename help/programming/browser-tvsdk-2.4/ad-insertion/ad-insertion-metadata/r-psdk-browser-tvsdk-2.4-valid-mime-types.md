---
description: 一个广告可能具有多个创意，其中有一个被选择播放。
title: 有效的MIME类型
exl-id: 878cae20-2a94-4795-8908-be7daffefb41
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# 有效的MIME类型{#valid-mime-types}

一个广告可能具有多个创意，其中有一个被选择播放。

对于MIME类型，您可以指定用户可以优先考虑哪些创意类型。 用户指定的mime类型以及浏览器TVSDK支持的mime类型用于确定将优先处理哪些创意。

要在浏览器TVSDK中设置有效的MIME类型，请执行以下操作：

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

位置 `mimeTypes` 是一个字符串数组，每个字符串都表示一种mime类型。

如果为广告返回多个媒体文件，则选择取决于媒体文件在其中出现的顺序 `validMimeTypes` 数组。 索引较低的mime类型比索引较高的类型优先。
