---
description: 全事件重播(FER)是充当实时/DVR资产的VOD资产，因此您的应用程序必须采取步骤来确保正确放置广告。
seo-description: 全事件重播(FER)是充当实时/DVR资产的VOD资产，因此您的应用程序必须采取步骤来确保正确放置广告。
seo-title: 支持全事件重播广告
title: 支持全事件重播广告
uuid: 69244069-ef61-42e4-b2f5-62ae2561d9e1
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# 启用全事件重播{#enable-ads-in-full-event-replay-overview}中的广告

全事件重播(FER)是充当实时/DVR资产的VOD资产，因此您的应用程序必须采取步骤来确保正确放置广告。

对于实时内容，TVSDK使用清单中的元数据／提示确定广告的放置位置。 但是，有时实时／线性内容可能与VOD内容类似。 例如，当实时内容完成时，将向实时清单附加一个`EXT-X-ENDLIST`标记。 对于HLS,`EXT-X-ENDLIST`标记表示流是VOD流。 要正确插入广告，TVSDK无法自动将此流与典型VOD流区分开。

应用程序必须通过指定`AdSignalingMode`来告诉TVSDK内容是实时的还是VOD的。

对于FER流，Adobe Primetime广告决策服务器不应提供在开始播放之前需要在时间轴上插入的广告中断的列表。 这是VOD内容的典型过程。 相反，通过指定不同的信令模式，TVSDK从FER清单读取所有提示点并转到广告服务器以请求广告中断。 此过程类似于实时/DVR内容。

>[!TIP]
>
>除了与提示点关联的每个请求外，TVSDK还对预放广告提出额外的广告请求。

1. 从外部源（如vCMS）获得应使用的信令模式。
1. 创建与广告相关的元数据。
1. 如果必须覆盖默认行为，请使用`AdvertisingMetadata.setSignalingMode`指定`AdSignalingMode`。

   有效值为`DEFAULT`、`SERVER_MAP`和`MANIFEST_CUES`。

   >[!IMPORTANT]
   >
   >在调用`prepareToPlay`之前，必须设置广告信令模式。 在TVSDK开始解析广告并将其放在时间轴上后，将忽略对广告信号模式所做的更改。 在创建`AuditudeSettings`对象时设置模式。

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
