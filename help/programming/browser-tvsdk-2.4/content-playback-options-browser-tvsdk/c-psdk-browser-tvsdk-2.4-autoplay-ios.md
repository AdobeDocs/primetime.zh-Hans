---
title: 在iOS上自动播放
description: 在iOS上自动播放
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---


# 在iOS上自动播放{#autoplay-on-ios}

通过实施AdobePSDK.MediaPlayer的卷API，可以在运行iOS版本10或更高版本的设备上自动播放内容。 iOS仅允许在静音卷时自动播放。 当卷设置为零时，API将视频标签的`muted`属性设置为`true`，否则将`muted`属性设置为`false`。 `play` API将播放开始，无需任何用户交互或用户手势。

对于iPhone上的自动播放，还可将`video`标签的`playsInline`属性设置为`true`。

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>使用`playsInline`属性可开始播放而不使用全屏模式。

