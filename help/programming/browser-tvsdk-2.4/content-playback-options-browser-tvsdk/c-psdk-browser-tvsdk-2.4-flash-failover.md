---
description: 浏览器TVSDK提供了用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。
title: Flash故障转移
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Flash故障转移 {#flash-failover}

浏览器TVSDK提供了用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。

使用您平台的工具来创建播放器，并将其连接到浏览器TVSDK中的媒体播放器视图，该视图提供了多种播放和管理视频的方法。 例如，浏览器TVSDK提供播放和暂停方法。 您可以在平台上创建用户界面按钮，并设置这些按钮以调用浏览器TVSDK方法。

## Flash回退 {#section_92D3884A13A6431F9A9CC5C79715D888}

在浏览器TVSDK中，您的应用程序仅与 `Primetime.js` API。 底层浏览器TVSDK实现根据当前平台和待播放媒体的资源类型来决定使用哪种播放器技术。

直到您调用，才会做出播放器技术的决定 `MediaPlayer.replaceCurrentResource` 播放特定资源。

例如：

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## 确定要使用的媒体播放器 {#section_D844E386AF5848688D204DEE258ECEE6}

此示例过程说明了确定播放器技术的过程：

>[!TIP]
>
>此过程可能会因URL和您的环境而异。

1. 如果支持媒体源扩展，则使用它时没有已知限制。
1. 如果受支持，请使用 `<video>` 不使用MSE直接标记。
1. 确保您至少使用AdobeFlash Player版本23.0。
1. 如果找不到合适的回放技术， `replaceCurrentResource` 返回错误。

后续的 `replaceCurrentResource` 在同一台计算机上调用 `MediaPlayer` 实例遵循相同的过程。 这允许您使用播放器播放各种资源类型 `MediaPlayer` 同一父级中的实例 `<DIV>` 您指定的标记 `MediaPlayerView` 实例已创建。

>[!TIP]
>
>SWF对象和 `<video>` 标记嵌套在父项中 `<DIV>` 标记之前。
