---
description: 替代或延迟绑定音频允许您在视频轨道的可用音轨之间切换。 这样，用户可以在播放视频时选择语言轨道。
seo-description: 替代或延迟绑定音频允许您在视频轨道的可用音轨之间切换。 这样，用户可以在播放视频时选择语言轨道。
seo-title: 替代音频
title: 替代音频
uuid: 9dc3bec6-2135-4083-8db2-50a492e6bd67
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 概述 {#alternate-audio-overview}

替代或延迟绑定音频允许您在视频轨道的可用音轨之间切换。 这样，用户可以在播放视频时选择语言轨道。

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

当TVSDK为当前视 `MediaPlayerItem` 频创建实例时，它会为每个可用 `AudioTrack` 的音轨创建一个项。 项目包含一个 `name` 属性，该字符串通常包含用户可识别的该轨道语言的描述。 该项目还包含有关是否默认使用该轨道的信息。

当需要播放视频时，您可以请求可用音轨列表，或者让用户选择一个音轨，并设置要与所选音轨一起播放的视频。

虽然很少，但如果在创建音轨后有其他音轨可用， `MediaPlayerItem`TVSDK会触发事 `MediaPlayerItem.AUDIO_UPDATED` 件。

## 添加的API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

已添加以下API以支持备用音频：

`hasAlternateAudio`

如果指定的媒体有除默认音轨之外的备用音轨，则此布尔函数将返回 `true`。 如果没有替代音轨，则函数返回 `false`。

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

此函数返回当前选择的替代音轨和属性，如语言。 还可以提取轨道的自动选择。

```
PSDKErrorCode MediaPlayerItemImpl::getSelectedAudioTrack(AudioTrack &out) const 
{ 
    out = _currentAudioTrack; 
    return kECSuccess; 
}
```

`selectAudioTrack`

此函数选择要播放的备用音轨。

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

