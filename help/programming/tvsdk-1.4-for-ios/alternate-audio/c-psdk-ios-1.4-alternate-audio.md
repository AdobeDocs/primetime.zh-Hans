---
description: 备用或延迟绑定的音频允许您在视频曲目的可用音频曲目之间切换。 通过这种方式，用户可以在播放视频时选择语言跟踪。
title: 备用音频
exl-id: c8158888-2e2a-42a6-a948-dc6ba4ce7a9c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 概述 {#alternate-audio-overview}

备用或延迟绑定的音频允许您在视频曲目的可用音频曲目之间切换。 通过这种方式，用户可以在播放视频时选择语言跟踪。

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

当TVSDK创建 `MediaPlayerItem` 对于当前视频的实例，它会创建 `AudioTrack` 每个可用音频轨道的项目。 该项包含 `name` 属性，一个字符串，通常包含用户可识别的对曲目语言的描述。 该项目还包含有关默认情况下是否使用该轨道的信息。

当播放视频时，您可以要求提供可用音轨的列表，可以选择让用户选择一个，然后将视频设置为使用所选音轨播放。

虽然很罕见，但如果附加音轨在创建 `MediaPlayerItem`，TVSDK触发 `MediaPlayerItem.AUDIO_UPDATED` 事件。

## 添加的API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

已添加以下API以支持备用音频：

`hasAlternateAudio`

如果指定的媒体有默认音轨以外的备用音轨，此布尔函数将返回 `true`. 如果没有替代音轨，则函数返回 `false`.

```
bool MediaPlayerItemImpl::hasAlternateAudio() const 
{ 
    return _hasAlternateAudio; 
}
```

** `getAudioTracks`**

此函数返回指定媒体中所有当前可用音轨的列表。

```
virtual PSDKErrorCode getAudioTracks(PSDKImmutableArray<AudioTrack>*& out) const 
    { 
        if (_audioTracks) 
        { 
            out = _audioTracks; 
            out->addRef(); 
            return kECSuccess; 
        } 
        return kECDataNotAvailable; 
    }
```

`getSelectedAudioTrack`

此函数返回当前选定的备用音频轨道和属性，例如语言。 也可提取轨迹的自动选择。

```
PSDKErrorCode MediaPlayerItemImpl::getSelectedAudioTrack(AudioTrack &out) const 
{ 
    out = _currentAudioTrack; 
    return kECSuccess; 
}
```

`selectAudioTrack`

此函数选择要播放的替代音轨。

```
PSDKErrorCode MediaPlayerItemImpl::selectAudioTrack(const AudioTrack &audioTrack) 
{ 
    _lastPlayedAudioTrack = _currentAudioTrack; 
    if(_mediaPlayer && _mediaPlayer->_trickPlay) 
        return kECUnsupportedOperation; 
    _currentAudioTrack = audioTrack; 
    PSDKErrorCode result = kECSuccess; 
    if (_currentAudioTrack) 
    { 
        media::TimeLine* timeline = NULL; 
        if (_mediaPlayer->_fragHttpStreamer) 
            _mediaPlayer->_fragHttpStreamer->GetTimeLine(&timeline); 
        if (timeline) 
        { 
            for (int32_t i = timeline->GetFirstPeriodIndex(); i <= timeline->GetLastPeriodIndex(); i++){ 
                media::ErrorCode error = selectTrack(timeline,_mediaPlayer->_fragHttpStreamer, i, audioTrack.getName(), media::kSTTAudioIndex); 
                return _mediaPlayer->convertToPSDKError(error); 
            } 
        } 
    }   
    return result; 
}
```
