---
description: 替代音频允许您在视频轨道的可用音轨之间切换。 用户可以在播放视频时选择其首选语言轨道。
seo-description: 替代音频允许您在视频轨道的可用音轨之间切换。 用户可以在播放视频时选择其首选语言轨道。
seo-title: 替代音频
title: 替代音频
uuid: 86aa5393-6a9e-49db-807b-7299e6b4ab2b
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 概述 {#alternate-audio-overview}

替代音频允许您在视频轨道的可用音轨之间切换。 用户可以在播放视频时选择其首选语言轨道。

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

当TVSDK为当前视 `MediaPlayerItem` 频创建实例时，它会为每个可用 `AudioTrack` 的音轨创建一个项。 项目包含一个 `name` 属性，该属性是一个字符串，通常包含用户可识别的该轨道语言的描述。 该项目还包含有关是否默认使用该轨道的信息。 当需要播放视频时，您可以请求可用音轨列表，或者允许用户选择一条轨道，并设置视频以与所选轨道一起播放。

>[!TIP]
>
>虽然很少，但如果TVSDK创建后有其他音轨可用， `MediaPlayerItem`则TVSDK将触发事 `MediaPlayerItem.AUDIO_TRACK_UPDATED` 件。

## 添加的API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

已添加以下API以支持备用音频：

`hasAlternateAudio`

如果指定的媒体有除默认音轨之外的备用音轨，则此布尔函数将返回 `true`。 如果没有替代音轨，则函数返回 `false`。

```java
boolean hasAlternateAudio();
```

** `getAudioTracks`**

此函数返回指定媒体中所有当前可用音轨的列表。

```java
List<AudioTrack> getAudioTracks();
```

`getSelectedAudioTrack`

此函数返回当前选择的替代音轨和属性，如语言。 还可以提取轨道的自动选择。

```java
AudioTrack getSelectedAudioTrack();
```

`selectAudioTrack`

此函数选择要播放的备用音轨。

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

