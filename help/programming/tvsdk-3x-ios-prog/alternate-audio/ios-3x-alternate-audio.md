---
title: 备用音频
description: 备用音频
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 备用音频 {#alternate-audio}

备用或延迟绑定的音频允许您在视频轨道的可用音频轨道之间切换。 这样，用户就可以在播放视频时选择语言跟踪。

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

当TVSDK创建 `MediaPlayerItem` 对于当前视频的实例，它会创建 `AudioTrack` 每个可用音轨的项目。 该项包含 `name` 属性，一个字符串，通常包含该轨道的语言的用户可识别描述。 该项还包含有关默认情况下是否使用该轨道的信息。

当播放视频时，您可以要求提供可用音轨的列表，也可以让用户选择可用音轨，然后设置视频以使用所选音轨播放。

虽然很少，但如果创建后有其他音频轨道可用， `MediaPlayerItem`， TVSDK触发 `MediaPlayerItem.AUDIO_UPDATED` 事件。

## 添加的API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

已添加以下API以支持备用音频：

**hasAlternateAudio**

如果指定的媒体有默认音轨以外的备用音轨，则此布尔函数返回 `true`. 如果没有备用音轨，则函数返回 `false`.

```
bool MediaPlayerItemImpl::hasAlternateAudio() const { 
    return _hasAlternateAudio; 
}
```

**getAudioTracks**

此函数返回指定媒体中所有当前可用声道的列表。

```
virtual PSDKErrorCode getAudioTracks(PSDKImmutableArray<AudioTrack>*& out) const { 
    if (_audioTracks) { 
        out = _audioTracks; 
        out->addRef(); 
        return kECSuccess; 
    } 
    return kECDataNotAvailable; 
} 
```

**getSelectedAudioTrack**

此函数返回当前所选的备用音频轨道和属性，如语言。 也可提取轨迹的自动选取。

```
PSDKErrorCode MediaPlayerItemImpl::getSelectedAudioTrack(AudioTrack &out) const { 
    out = _currentAudioTrack; 
    return kECSuccess; 
}
```

**selectAudioTrack**

此函数选择要播放的备用音轨。

```
PSDKErrorCode MediaPlayerItemImpl::selectAudioTrack(const AudioTrack &audioTrack) { 
    _lastPlayedAudioTrack = _currentAudioTrack; 
    if(_mediaPlayer && _mediaPlayer->_trickPlay) 
        return kECUnsupportedOperation; 
    _currentAudioTrack = audioTrack; 
    PSDKErrorCode result = kECSuccess; 
    if (_currentAudioTrack) { 
        media::TimeLine* timeline = NULL; 
        if (_mediaPlayer->_fragHttpStreamer) 
            _mediaPlayer->_fragHttpStreamer->GetTimeLine(&timeline); 
        if (timeline) { 
            for (int32_t i = timeline->GetFirstPeriodIndex(); i <= timeline->GetLastPeriodIndex(); i++){ 
                media::ErrorCode error = selectTrack(timeline,_mediaPlayer->_fragHttpStreamer, i, audioTrack.getName(), media::kSTTAudioIndex); 
                return _mediaPlayer->convertToPSDKError(error); 
            } 
        } 
    }   
    return result; 
}
```
