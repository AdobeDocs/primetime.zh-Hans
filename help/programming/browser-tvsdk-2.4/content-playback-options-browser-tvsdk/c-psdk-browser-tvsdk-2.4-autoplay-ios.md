---
description: 'null'
seo-description: 'null'
seo-title: 在iOS上自动播放
title: 在iOS上自动播放
uuid: d15bad24-be50-49e5-90f4-68dbda96fb6d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 在iOS上自动播放{#autoplay-on-ios}

AdobePSDK.MediaPlayer的卷API的实施允许在运行iOS版本10或更高版本的设备上自动播放内容。 iOS仅允许在静音时自动播放。 当卷设置为零时，API将视频标 `muted` 签的属性设置为 `true`，否则 `muted` 将属性设置为 `false`。 该 `play` API无需任何用户交互或用户手势即可启动播放。

对于在iPhone上自动播放，另外将标 `playsInline` 记的属性设 `video` 置为 `true`。

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>使用属 `playsInline` 性可在不使用全屏模式的情况下开始播放。

