---
description: 浏览器TVSDK提供用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。
seo-description: 浏览器TVSDK提供用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。
seo-title: 'null'
title: 'null'
uuid: 57b35a5f-87f8-41a2-ad85-300b999dc30b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Flash故障转移 {#flash-failover}

浏览器TVSDK提供用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。

使用平台的工具创建播放器并将其连接到浏览器TVSDK中的媒体播放器视图，该视图具有播放和管理视频的方法。 例如，浏览器TVSDK提供播放和暂停方法。 您可以在平台上创建用户界面按钮并设置按钮以调用这些浏览器TVSDK方法。

## Flash回退 {#section_92D3884A13A6431F9A9CC5C79715D888}

在浏览器TVSDK中，您的应用程序仅与API `Primetime.js` 交互。 底层浏览器TVSDK实现根据当前平台和要播放的媒体的资源类型决定要使用的播放器技术。

只有在您调用播放特定资源之前，才会决 `MediaPlayer.replaceCurrentResource` 定播放器技术。

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
>该过程可能因URL和环境而异。

1. 如果支持媒体源扩展，则使用它时没有已知限制。
1. 如果支持，请直接使 `<video>` 用不带MSE的标签。
1. 确保您至少使用Adobe Flash Player版本23.0。
1. 如果找不到合适的播放技术， `replaceCurrentResource` 则返回错误。

对同一实 `replaceCurrentResource` 例的后续调用会 `MediaPlayer` 遵循相同的进程。 这允许您通过在创建实例时指定的同一父标 `MediaPlayer` 签中使用同一实例来播 `<DIV>` 放各种资源 `MediaPlayerView` 类型。

>[!TIP]
>
>SWF对象和标 `<video>` 签嵌套在父标签 `<DIV>` 中。

