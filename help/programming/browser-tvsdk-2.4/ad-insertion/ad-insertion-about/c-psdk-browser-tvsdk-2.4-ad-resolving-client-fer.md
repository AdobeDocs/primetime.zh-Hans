---
description: 完整事件重放(FER)内容是通过将#EXT-X-ENDLIST标记添加到清单文件的末尾来转换为VOD的实时流。 流保留其广告提示标记。
title: FER广告解析和插入
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# FER广告解析和插入{#fer-ad-resolving-and-insertion}

完整事件重放(FER)内容是通过将#EXT-X-ENDLIST标记添加到清单文件的末尾来转换为VOD的实时流。 流保留其广告提示标记。

浏览器TVSDK将FER流视为VOD，因此默认情况下，广告信令模式为 `SERVER_MAP`. 但是，由于流保留其广告提示标记，因此您可以将广告信令模式设置为 `MANIFEST_CUES`，这让您能够使用广告提示标记进行广告插入。

要为FER流使用提示标记打开广告插入，请执行以下操作：

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

FER广告解析和插入行为类似于实时广告解析和插入。 浏览器TVSDK执行以下操作：

1. 在内容的开头插入任何前置广告。
1. 解析由清单中定义的提示点指定的广告。
1. 用相同持续时间的广告时间替换部分主内容
1. 如有必要，重新计算虚拟时间线。

**限制：** 浏览器TVSDK仅支持HLS FER流播放。 此外，FER流不支持MP4中置广告。
