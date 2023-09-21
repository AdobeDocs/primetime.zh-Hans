---
title: 在iOS上自动播放
description: 在iOS上自动播放
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# 在iOS上自动播放{#autoplay-on-ios}

AdobePSDK.MediaPlayer的卷API的实现允许在运行iOS版本10或更高版本的设备上自动播放内容。 iOS仅在音量静音时允许自动播放。 当卷设置为零时，API将 `muted` 将视频标记的属性设置为 `true`，否则 `muted` 属性设置为 `false`. 此 `play` API无需进行任何用户交互或用户手势即可开始播放。

对于在iPhone上自动播放，请另外设置 `playsInline` 的属性 `video` 标记至 `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>使用 `playsInline` 属性在没有全屏模式的情况下开始播放。
