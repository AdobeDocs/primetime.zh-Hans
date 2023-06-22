---
description: 完整事件重播(FER)是一种充当实时/DVR资源的VOD资源，因此您的应用程序必须采取措施以确保正确放置广告。
title: 在全事件重放中启用广告
exl-id: d6f7efc9-48f4-4101-a425-c354557cdd4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 在全事件重放中启用广告{#enable-ads-in-full-event-replay}

完整事件重播(FER)是一种充当实时/DVR资源的VOD资源，因此您的应用程序必须采取措施以确保正确放置广告。

对于实时内容，TVSDK使用清单中的元数据/提示来确定放置广告的位置。 但是，有时实时/线性内容可能与VOD内容类似。 例如，当实时内容完成时， `EXT-X-ENDLIST` 标记将附加到实时清单中。 对于HLS，使用 `EXT-X-ENDLIST` 标记表示该流是VOD流。 TVSDK无法自动区分此流与正常VOD流以正确插入广告。

您的应用程序必须指定 `AdSignalingMode`.

对于FER流，Adobe Primetime ad decisioning服务器不应提供在开始播放之前需要插入到时间轴上的广告时间的列表。 这是VOD内容的典型过程。 相反，通过指定不同的信令模式，TVSDK从FER清单中读取所有提示点，并且对于每个提示点转到广告服务器以请求广告中断。 此过程类似于实时/DVR内容。

除了与提示点关联的每个请求之外，TVSDK还针对前置广告提出额外的广告请求。

1. 从外部源（如vCMS）获取应使用的信令模式。
1. 创建与广告相关的元数据。
1. 如果必须覆盖默认行为，请指定 `AdSignalingMode` 通过使用 `AdvertisingMetadata.setSignalingMode`.

   有效值为 `DEFAULT, SERVER_MAP`、和 `MANIFEST_CUES`.

   在调用之前，必须设置广告信号模式 `prepareToPlay`. 在TVSDK开始解析广告并将广告置于时间轴上后，对广告信号模式的更改将被忽略。 创建时设置模式 `AuditudeSettings` 对象。

1. 继续播放。

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->
