---
description: 完整事件重播(FER)内容是通过将#EXT-X-ENDLIST标签添加到清单文件末尾而转换为VOD的实时流。 该流保留其广告提示标记。
seo-description: 完整事件重播(FER)内容是通过将#EXT-X-ENDLIST标签添加到清单文件末尾而转换为VOD的实时流。 该流保留其广告提示标记。
seo-title: FER广告解析和插入
title: FER广告解析和插入
uuid: 85da0e92-17fe-4001-a53c-085dadd09756
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# FER广告解析和插入{#fer-ad-resolving-and-insertion}

完整事件重播(FER)内容是通过将#EXT-X-ENDLIST标签添加到清单文件末尾而转换为VOD的实时流。 该流保留其广告提示标记。

浏览器TVSDK将FER流视为VOD，因此默认情况下，广告信号模式为`SERVER_MAP`。 但是，由于流保留其广告提示标记，您可以将广告信号模式设置为`MANIFEST_CUES`，这样您就可以使用广告提示标记进行广告插入。

要使用FER流的提示标记打开广告插入：

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

FER广告解析和插入行为与实时广告解析和插入类似。 浏览器TVSDK执行以下操作：

1. 在内容的开头插入任何预放广告。
1. 解析由清单中定义的提示点指定的广告。
1. 用相同持续时间的广告分段替换部分主内容
1. 如有必要，重新计算虚拟时间轴。

**限制：** 浏览器TVSDK仅支持HLS FER流播放。此外，FER流不支持MP4中间广告。
