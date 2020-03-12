---
description: 完全事件重播(FER)是一个充当实时/DVR资产的VOD资产，因此您的应用程序必须采取步骤来确保正确放置广告。
seo-description: 完全事件重播(FER)是一个充当实时/DVR资产的VOD资产，因此您的应用程序必须采取步骤来确保正确放置广告。
seo-title: 在全场重播中启用广告
title: 在全场重播中启用广告
uuid: a8859db1-1408-4365-bf12-5bc2ab7df449
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 在全场重播中启用广告 {#enable-ads-in-full-event-replay}

完全事件重播(FER)是一个充当实时/DVR资产的VOD资产，因此您的应用程序必须采取步骤来确保正确放置广告。

对于实时内容，TVSDK使用清单中的元数据／提示确定广告的放置位置。 但是，有时实时／线性内容可能与VOD内容类似。 例如，当活动内容完成时，将 `EXT-X-ENDLIST` 向活动清单附加一个标记。 对于HLS，标 `EXT-X-ENDLIST` 记表示流是VOD流。 要正确插入广告，TVSDK无法自动将此流与典型的VOD流区分开来。

您的应用程序必须通过指定内容来告诉TVSDK内容是实时的还是VOD的 `AdSignalingMode`。

对于FER流，Adobe Primetime广告决策服务器不应提供在开始播放之前需要在时间轴上插入的广告分段列表。 这是VOD内容的典型过程。 相反，通过指定不同的信令模式，TVSDK从FER清单中读取所有提示点并转到每个提示点的广告服务器以请求广告中断。 此过程类似于实时/DVR内容。

>[!TIP]
>
>除了与提示点关联的每个请求之外，TVSDK还对前置广告发出额外的广告请求。

1. 从外部源（如vCMS）获得应使用的信令模式。
1. 创建与广告相关的元数据。
1. 如果必须覆盖默认行为，请使 `AdSignalingMode` 用指定 `AdvertisingMetadata.setSignalingMode`。

   有效值为 `DEFAULT`、 `SERVER_MAP`和 `MANIFEST_CUES`。

   >[!IMPORTANT]
   >
   >您必须先设置广告信令模式，然后再进行呼叫 `prepareToPlay`。 在TVSDK开始解析广告并将其放在时间轴上后，将忽略对广告信令模式的更改。 在创建对象时设置模 `AuditudeSettings` 式。

1. 继续播放。

<!--<a id="example_6DECA71C3C3B4551805C09A80686552F"></a>-->

```java
MediaPlayer mediaPlayer =  
  new MediaPlayer(getActivity.().getApplicationContext()); 
 
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings.setSignalingMode(AdSignalingMode.MANIFEST_CUES); 
auditudeSettings.setDomain("your-auditude-domain"); 
auditudeSettings.setZoneId("your-auditude-zone-id"); 
auditudeSettings.setMediaId("your-media-id"); 
// set additional targeting parameters or custom parameters 
 
MediaPlayerItemConfig itemConfig =  
  new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
MediaResource mediaResource =  
  new MediaResource("https://example.com/media/test_media.m3u8",  
                    MediaResource.Type.HLS, Metadata); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (status == MediaPlayerStatus.INITIALIZED) { 
            mediaPlayer.prepareToPlay(); 
        } 
        else if( event.getStatus() == MediaPlayerStatus.PREPARED ) { 
            // TVSDK is in the PREPARED state, so start the playback 
            mediaPlayer.play(); 
        } 
        else if( event.getStatus() == MediaPlayerStatus.COMPLETE ) { 
            // playback has reached the end of stream ( ads included ) 
            // if we want to rewind we can call 
            mediaPlayer.seek(mediaPlayer.getSeekableRange().getBegin()); 
        } 
    } 
}); 
 
mediaPlayer.replaceCurrentResource(mediaResource, itemConfig); 
```
