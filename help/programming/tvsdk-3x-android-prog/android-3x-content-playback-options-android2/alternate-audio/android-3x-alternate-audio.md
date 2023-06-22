---
description: 备用音频允许您在视频曲目的可用音频曲目之间切换。 用户可以在播放视频时选择其首选语言跟踪。
title: 备用音频
exl-id: 7438d667-3003-42ba-88f3-818fa093c7d9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# 概述 {#alternate-audio-overview}

备用音频允许您在视频曲目的可用音频曲目之间切换。 用户可以在播放视频时选择其首选语言跟踪。

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

当TVSDK创建 `MediaPlayerItem` 对于当前视频的实例，它会创建 `AudioTrack` 每个可用音频轨道的项目。 该项包含 `name` 属性，这是一个字符串，通常包含用户可识别的对曲目语言的描述。 该项目还包含有关默认情况下是否使用该轨道的信息。 当播放视频时，您可以要求提供可用音轨的列表，可以选择允许用户选择音轨，并将视频设置为使用所选音轨播放。

>[!TIP]
>
>虽然很少，但如果TVSDK创建音频之后 `MediaPlayerItem`，TVSDK触发 `MediaPlayerItem.AUDIO_TRACK_UPDATED` 事件。

## 添加的API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

已添加以下API以支持备用音频：

**`hasAlternateAudio`**

如果指定的媒体有默认音轨以外的备用音轨，此布尔函数将返回 `true`. 如果没有替代音轨，则函数返回 `false`.

```java
boolean hasAlternateAudio();
```

**`getAudioTracks`**

此函数返回指定媒体中所有当前可用音轨的列表。

```java
List<AudioTrack> getAudioTracks();
```

**`getSelectedAudioTrack`**

此函数返回当前选定的备用音频轨道和属性，例如语言。 也可提取轨迹的自动选择。

```java
AudioTrack getSelectedAudioTrack();
```

**`selectAudioTrack`**

此函数选择要播放的替代音轨。

```java
void selectAudioTrack(AudioTrack audioTrack);
```

例如：

```java
private void onPrepared() { 
    // Select the AA track in PREPARED State 
    boolean hasAlternateAudio = _mediaPlayer.getCurrentItem().hasAlternateAudio(); 
    if(hasAlternateAudio) { 
        AudioTrack selectedAudioTrack =  
          _mediaPlayer.getCurrentItem().getSelectedAudioTrack(); 
 
        if (selectedAudioTrack == null) {  
            // Selecting default audio track  
            // If index is 1 it will select alternate audio track  
            selectedAudioTrack = _mediaPlayer.getCurrentItem().getAudioTracks().get(0);  
        } 
    } 
    _mediaPlayer.getCurrentItem().selectAudioTrack(selectedAudioTrack); 
} 
```
