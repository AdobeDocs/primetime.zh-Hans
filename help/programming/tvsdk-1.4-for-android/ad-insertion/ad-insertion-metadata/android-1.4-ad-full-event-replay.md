---
description: 全事件重播(FER)是一个VOD资产，充当实时/DVR资产，因此您的应用程序必须采取步骤以确保正确放置广告。
title: 实现全事件重播
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---


# 启用全事件重播中的广告{#enable-ads-in-full-event-replay}

全事件重播(FER)是一个VOD资产，充当实时/DVR资产，因此您的应用程序必须采取步骤以确保正确放置广告。

对于实时内容，TVSDK使用清单中的元数据/提示确定放广告的位置。 但是，有时实时/线性内容可能与VOD内容相似。 例如，当活动内容完成时，将向活动清单附加一个`EXT-X-ENDLIST`标记。 对于HLS，`EXT-X-ENDLIST`标记表示流是VOD流。 TVSDK无法自动区分此流与普通VOD流，以正确插入广告。

应用程序必须通过指定`AdSignalingMode`来告诉TVSDK内容是实时的还是VOD的。

对于FER流，Adobe Primetime广告决策服务器不应提供在开始播放之前需要在时间轴上插入的广告中断的列表。 这是VOD内容的典型过程。 相反，通过指定不同的信令模式，TVSDK从FER清单读取所有提示点并转到每个提示点的广告服务器以请求广告中断。 此过程类似于实时/DVR内容。

除了与提示点关联的每个请求外，TVSDK还对前放广告发出额外的广告请求。

1. 从外部源（如vCMS）获得应使用的信令模式。
1. 创建与广告相关的元数据。
1. 如果必须覆盖默认行为，请使用`AdvertisingMetadata.setSignalingMode`指定`AdSignalingMode`。

   有效值为`DEFAULT, SERVER_MAP`和`MANIFEST_CUES`。

   在调用`prepareToPlay`之前，必须设置广告信令模式。 在TVSDK开始解析广告并将其放置到时间轴上后，将忽略对广告信号模式的更改。 在创建`AuditudeSettings`对象时设置模式。

1. 继续播放。

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->

