---
description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
seo-description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
seo-title: 用于访问MediaResource信息的MediaPlayerItem方法
title: 用于访问MediaResource信息的MediaPlayerItem方法
uuid: 46845583-0a76-4411-a8bc-0a16ebfe8e6e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 用于访问MediaResource信息的MediaPlayerItem方法 {#mediaplayeritem-methods-for-accessing-mediaresource-information}

MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。

| 方法 | 说明 |
|--- |--- |
| **广告标记** |  |
| 列出`<String>` getAdTags() | 提供用于广告投放过程的广告标记列表。 |
| **实时流** |  |
| boolean isLive(); | 如果流是实时的，则为true;如果为VOD，则为false。 |
| **DRM受保护** |  |
| boolean isProtected(); | 如果流受DRM保护，则为true。 |
| 列出`<DRMMetadataInfo>` getDRMMetadataInfos(); | 列出清单中发现的所有DRM元数据对象。 |
| **隐藏式字幕** |  |
| boolean hasClosedCaptions(); | 如果隐藏式字幕轨道可用，则为True。 |
| 列出`<ClosedCaptionsTrack>` getClosedConsitionsTracks(); | 提供可用隐藏式字幕轨道列表。 |
| ClosedCaptionsTrack获取SelectedClosedCaptionsTrack(); | 检索使用SelectClosedCaptionsTrack选择的当前隐藏字幕轨道。 |
| selectClosedCaptionsTrack(ClosedCaptionsTrack closedCaptionsTrack) | 将隐藏式字幕轨道设置为当前隐藏式字幕轨道。 |
| **替代音轨** |  |
| boolean hasAlternateAudio(); | 如果流具有替代音轨，则为true。 注意： 主音轨（默认）也是替代音轨列表的一部分。  适用于Android的TVSDK将主音轨视为替代音轨列表中的项之一。 因此，MediaPlayerItem.hasAlternateAudio返回false的唯一情况是当流根本没有音频时。 如果内容只有一个音轨，则此方法返回true，并 `MediaPlayerItem.getAudioTracks` 返回包含单个元素（默认音轨）的列表。 |
| 列出`<AudioTrack>` getAudioTracks(); | 提供可用替代音轨的列表。 |
| AudioTrack getSelectedAudioTrack(); | 检索使用selectAudioTrack选择的音轨。 |
| selectAudioTrack(AudioTrack audioTrack) | 选择音轨作为当前音轨。 |
| **定时元数据** |  |
| boolean hasTimedMetadata(); | 如果流已关联定时元数据，则为true。 |
| 列出`<TimedMetadata>` getTimedMetadata(); | 提供与流关联的定时元数据对象的列表。 |
| **多个配置文件（位速率）** |
| boolean isDynamic(); | 如果流是多位速率(MBR)流，则为true。 |
| 列出`<Profile>` getProfiles(); | 提供关联的比特率配置文件列表。 对于每个配置文件，您可以检索其位速率以及配置文件的高度和宽度。 |
| 配置文件getSelectedProfile() | 检索当前选定的配置文件。 |
| **特技播放** |  |
| boolean isTrickPlaySupported(); | 如果播放器支持快速前进、后退和恢复，则为true。 |
| 列出`< Float>` getAvailablePlaybackRates() | 提供特技播放功能上下文中的可用播放速率列表。 |
| 浮动getSelectedPlaybackRate() | 检索当前选定的播放速率。 |
| MediaPlayerItemConfig getConfig() | 返回与此项目关联的MediaPlayerItemConfig实例。 |
| **媒体资源** |  |
| MediaResource getResource(); | 返回与此项目关联的媒体资源。 |
| int getResourceId() | 返回与此项目关联的媒体标识符。 使用MediaPlayerItemLoader.load加载项目时设置此ID。 |