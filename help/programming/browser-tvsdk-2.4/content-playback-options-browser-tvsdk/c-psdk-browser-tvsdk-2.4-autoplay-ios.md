---
description: 'null'
seo-description: 'null'
seo-title: 在iOS上自动播放
title: 在iOS上自动播放
uuid: d15bad24-be50-49e5-90f4-68dbda96fb6d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# 在iOS上自动播放{#autoplay-on-ios}

AdobePSDK.MediaPlayer的卷API的实施允许在运行iOS版本10或更高版本的设备上自动播放内容。 iOS仅在静音时允许自动播放。 当卷设置为零时，API将视频标记的`muted`属性设置为`true`，否则将`muted`属性设置为`false`。 `play` API开始播放，无需任何用户交互或用户手势。

对于iPhone上的自动播放，还可将`video`标记的`playsInline`属性设置为`true`。

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>使用`playsInline`属性将播放与全屏模式开始。

