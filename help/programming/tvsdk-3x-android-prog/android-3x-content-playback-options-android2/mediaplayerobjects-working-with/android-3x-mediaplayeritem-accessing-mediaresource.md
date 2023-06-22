---
description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
title: 用于访问MediaResource信息的MediaPlayerItem方法
exl-id: d6a547f3-0267-4a49-93a4-628b4879aef4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# 用于访问MediaResource信息的MediaPlayerItem方法 {#mediaplayeritem-methods-for-accessing-mediaresource-information}

MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。

| 方法 | 描述 |
|--- |--- |
| **广告标记** |  |
| 列表`<String>` getAdTags() | 提供用于广告投放流程的广告标记列表。 |
| **实时流** |  |
| 布尔值isLive()； | 如果流是实时的，则为true；如果是VOD，则为false。 |
| **受DRM保护** |  |
| 布尔值isProtected()； | 如果流受DRM保护，则为True。 |
| 列表`<DRMMetadataInfo>` getDRMMetadataInfos()； | 列出清单中发现的所有DRM元数据对象。 |
| **隐藏字幕** |  |
| 布尔型hasClosedCaptions()； | 如果隐藏式字幕跟踪可用，则为True。 |
| 列表`<ClosedCaptionsTrack>` getClosedCationsTracks()； | 提供可用隐藏式字幕字幕的列表。 |
| ClosedCaptionsTrack get SelectedClosedCaptionsTrack()； | 检索通过SelectClosedCaptionsTrack选择的当前隐藏式字幕跟踪。 |
| selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) | 将隐藏式字幕轨迹设置为当前的隐藏式字幕轨迹。 |
| **备用音轨** |  |
| 布尔值hasAlternateAudio()； | 如果流具有备用音轨，则为True。 注意：主（默认）音轨也是备用音轨列表的一部分。  适用于Android的TVSDK将主音频轨道视为备用音频轨道列表中的项目之一。 因此，MediaPlayerItem.hasAlternateAudio返回false的唯一情况是流完全没有音频。 如果内容只有一个音轨，则此方法返回true，并且  `MediaPlayerItem.getAudioTracks`  返回带有单个元素（默认音轨）的列表。 |
| 列表`<AudioTrack>` getAudioTracks()； | 提供可用备用音轨的列表。 |
| AudioTrack getSelectedAudioTrack()； | 检索使用selectAudioTrack选择的音轨。 |
| selectAudioTrack ( AudioTrack audioTrack ) | 选择一个音轨作为当前音轨。 |
| **定时元数据** |  |
| 布尔型hasTimedMetadata()； | 如果流具有关联的定时元数据，则为True。 |
| 列表`<TimedMetadata>` getTimedMetadata()； | 提供与流关联的定时元数据对象列表。 |
| **多个配置文件（比特率）** |
| 布尔值isDynamic()； | 如果流是多比特率(MBR)流，则为True。 |
| 列表`<Profile>` getProfiles()； | 提供相关比特率配置文件的列表。 对于每个配置文件，您可以检索其比特率以及配置文件的高度和宽度。 |
| 配置文件getSelectedProfile() | 检索当前选定的配置文件。 |
| **特技游戏** |  |
| 布尔值isTrickPlaySupported()； | 如果播放器支持快进、倒带和恢复，则为True。 |
| 列表`< Float>` getAvailablePlaybackRates() | 提供特技播放功能上下文中的可用播放速率列表。 |
| 浮点数getSelectedPlaybackRate() | 检索当前选定的播放速率。 |
| MediaPlayerItemConfig getConfig() | 返回与此项目关联的MediaPlayerItemConfig实例。 |
| **媒体资源** |  |
| MediaResource getResource()； | 返回与此项目关联的媒体资源。 |
| int getResourceId() | 返回与此项目关联的媒体标识符。 当使用MediaPlayerItemLoader.load加载项目时，会设置此ID。 |
