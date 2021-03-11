---
description: 浏览器TVSDK提供用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将该应用程序与其他Primetime组件集成。
title: Flash故障转移
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# Flash故障转移{#flash-failover}

浏览器TVSDK提供用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将该应用程序与其他Primetime组件集成。

使用您平台的工具创建播放器，并在浏览器TVSDK中将其连接到媒体播放器视图，该应用程序具有播放和管理视频的方法。 例如，Browser TVSDK提供播放和暂停方法。 您可以在平台上创建用户界面按钮并设置按钮以调用这些浏览器TVSDK方法。

## Flash回退{#section_92D3884A13A6431F9A9CC5C79715D888}

在浏览器TVSDK中，您的应用程序仅与`Primetime.js` API交互。 底层的Browser TVSDK实现根据当前平台和要播放的媒体的资源类型决定要使用的播放器技术。

在您调用`MediaPlayer.replaceCurrentResource`来播放特定资源之前，不会对播放器技术做出决定。

例如：

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## 确定要使用{#section_D844E386AF5848688D204DEE258ECEE6}的媒体播放器

此示例过程说明了确定播放器技术的过程：

>[!TIP]
>
>过程可能因URL和环境而异。

1. 如果支持媒体源扩展，请使用它并且不受已知限制。
1. 如果支持，请直接使用`<video>`标签，而不使用MSE。
1. 请确保您至少使用Adobe Flash Player版本23.0。
1. 如果找不到合适的播放技术，`replaceCurrentResource`将返回错误。

对同一个`MediaPlayer`实例的后续`replaceCurrentResource`调用遵循同一进程。 这允许您通过在创建`MediaPlayerView`实例时指定的相同父`<DIV>`标签中使用相同的`MediaPlayer`实例来播放各种资源类型。

>[!TIP]
>
>SWF对象和`<video>`标记嵌套在父`<DIV>`标记中。

