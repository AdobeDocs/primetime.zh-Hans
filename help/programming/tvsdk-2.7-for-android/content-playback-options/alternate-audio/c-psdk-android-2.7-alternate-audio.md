---
description: 替代音频允许您在视频轨道的可用音轨之间进行切换。 用户可以在播放视频时选择自己喜欢的语言轨道。
seo-description: 替代音频允许您在视频轨道的可用音轨之间进行切换。 用户可以在播放视频时选择自己喜欢的语言轨道。
seo-title: 替代音频
title: 替代音频
uuid: 86aa5393-6a9e-49db-807b-7299e6b4ab2b
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# 概述{#alternate-audio-overview}

替代音频允许您在视频轨道的可用音轨之间进行切换。 用户可以在播放视频时选择自己喜欢的语言轨道。

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

当TVSDK为当前视频创建`MediaPlayerItem`实例时，它为每个可用音轨创建`AudioTrack`项。 该项包含`name`属性，该属性是一个字符串，通常包含用户可识别的该音轨语言的描述。 该项目还包含有关是否默认使用该轨道的信息。 当需要播放视频时，您可以要求列表可用的音轨，或者允许用户选择一条音轨，并将视频设置为与所选音轨一起播放。

>[!TIP]
>
>虽然很少，但如果在TVSDK创建`MediaPlayerItem`后有其他音轨可用，则TVSDK将触发`MediaPlayerItem.AUDIO_TRACK_UPDATED`事件。

## 添加了API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

已添加以下API以支持备用音频：

`hasAlternateAudio`

如果指定的媒体具有除默认音轨之外的备用音轨，则此布尔函数返回`true`。 如果没有替代音轨，则函数返回`false`。

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

