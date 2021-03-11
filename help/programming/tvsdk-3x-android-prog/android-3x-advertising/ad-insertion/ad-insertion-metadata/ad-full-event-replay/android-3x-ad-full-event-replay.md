---
description: 全事件重播(FER)是一个VOD资产，充当实时/DVR资产，因此您的应用程序必须采取步骤以确保正确放置广告。
title: 实现全事件重播
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---


# 启用全事件重播{#enable-ads-in-full-event-replay}中的广告

全事件重播(FER)是一个VOD资产，充当实时/DVR资产，因此您的应用程序必须采取步骤以确保正确放置广告。

对于实时内容，TVSDK使用清单中的元数据/提示确定放广告的位置。 但是，有时实时/线性内容可能与VOD内容相似。 例如，当活动内容完成时，将向活动清单附加一个`EXT-X-ENDLIST`标记。 对于HLS，`EXT-X-ENDLIST`标记表示流是VOD流。 要正确插入广告，TVSDK无法自动区分此流与典型VOD流。

应用程序必须通过指定`AdSignalingMode`来告诉TVSDK内容是实时的还是VOD的。

对于FER流，Adobe Primetime广告决策服务器不应提供在开始播放之前需要在时间轴上插入的广告中断的列表。 这是VOD内容的典型过程。 相反，通过指定不同的信令模式，TVSDK从FER清单读取所有提示点并转到每个提示点的广告服务器以请求广告中断。 此过程类似于实时/DVR内容。

>[!TIP]
>
>除了与提示点关联的每个请求外，TVSDK还对前放广告发出额外的广告请求。

1. 从外部源（如vCMS）获得应使用的信令模式。
1. 创建与广告相关的元数据。
1. 如果必须覆盖默认行为，请使用`AdvertisingMetadata.setSignalingMode`指定`AdSignalingMode`。

   有效值为`DEFAULT`、`SERVER_MAP`和`MANIFEST_CUES`。

   >[!IMPORTANT]
   >
   >在调用`prepareToPlay`之前，必须设置广告信令模式。 在TVSDK开始解析广告并将其放置到时间轴上后，将忽略对广告信号模式的更改。 在创建`AuditudeSettings`对象时设置模式。

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
