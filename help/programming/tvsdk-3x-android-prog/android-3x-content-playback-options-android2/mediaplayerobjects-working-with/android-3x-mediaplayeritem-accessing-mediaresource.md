---
description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
title: 用于访问MediaResource信息的MediaPlayerItem方法
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---


# 用于访问MediaResource信息{#mediaplayeritem-methods-for-accessing-mediaresource-information}的MediaPlayerItem方法

MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。

| 方法 | 说明 |
|--- |--- |
| **广告标签** |  |
| 列表`<String>` getAdTags() | 提供用于广告投放流程的广告标签的列表。 |
| **实时流** |  |
| boolean isLive(); | 如果流是实时的，则为true;如果为VOD，则为false。 |
| **DRM受保护** |  |
| boolean isProtected(); | 如果流受DRM保护，则为true。 |
| 列表`<DRMMetadataInfo>` getDRMMetadataInfos(); | 列表清单中发现的所有DRM元数据对象。 |
| **隐藏式字幕** |  |
| boolean hasClosedCaptions(); | 如果隐藏字幕轨道可用，则为true。 |
| 列表`<ClosedCaptionsTrack>` getClosedActionsTracks(); | 提供可用隐藏字幕轨道的列表。 |
| ClosedCaptionsTrack获取SelectedClosedCaptionsTrack(); | 检索使用SelectClosedCaptionsTrack选择的当前隐藏字幕轨道。 |
| selectClosedCaptionsTrack(ClosedCaptionsTrack closedCaptionsTrack) | 将隐藏字幕轨道设置为当前隐藏字幕轨道。 |
| **替代音轨** |  |
| boolean hasAlternateAudio(); | 如果流具有替代音轨，则为true。 注意： 主音轨（默认）也是替代音轨列表的一部分。  适用于Android的TVSDK将主音轨视为备用音轨列表中的项目之一。 因此，MediaPlayerItem.hasAlternateAudio返回false的唯一情况是流中根本没有音频。 如果内容只有一个音轨，则此方法返回true，而`MediaPlayerItem.getAudioTracks`返回具有单个元素（默认音轨）的列表。 |
| 列表`<AudioTrack>` getAudioTracks(); | 提供可用替代音轨的列表。 |
| AudioTrack getSelectedAudioTrack(); | 检索使用selectAudioTrack选择的音轨。 |
| selectAudioTrack(AudioTrack audioTrack) | 选择音轨作为当前音轨。 |
| **定时元数据** |  |
| boolean hasTimedMetadata(); | 如果流具有关联的定时元数据，则为true。 |
| 列表`<TimedMetadata>` getTimedMetadata(); | 提供与流关联的定时元数据对象的列表。 |
| **多个用户档案（位速率）** |
| boolean isDynamic(); | 如果流是多比特率(MBR)流，则为true。 |
| 列表`<Profile>` getProfiles(); | 提供关联比特率列表用户档案。 对于每个用户档案，您可以检索其位速率以及用户档案的高度和宽度。 |
| 用户档案getSelectedProfile() | 检索当前选定的用户档案。 |
| **戏法** |  |
| boolean isTrickPlaySupported(); | 如果播放器支持快速前进、后退和恢复，则为true。 |
| 列表`< Float>` getAvailablePlaybackRates() | 在特技播放功能的上下文中提供可用播放速率的列表。 |
| 浮动getSelectedPlaybackRate() | 检索当前选定的播放速率。 |
| MediaPlayerItemConfig getConfig() | 返回与此项关联的MediaPlayerItemConfig实例。 |
| **媒体资源** |  |
| MediaResource getResource(); | 返回与此项目关联的媒体资源。 |
| int getResourceId() | 返回与此项目关联的媒体标识符。 使用MediaPlayerItemLoader.load加载项时将设置此ID。 |