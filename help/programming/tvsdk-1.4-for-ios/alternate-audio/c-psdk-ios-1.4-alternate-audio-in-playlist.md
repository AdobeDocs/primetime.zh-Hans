---
description: 视频的播放列表可以为主视频内容指定不限数量的替代音轨。 例如，您可能希望向视频内容添加不同的语言，或者允许用户在播放内容时在设备上的不同轨道之间切换。
title: 播放列表中的替代音轨
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# 播放列表中的替代音轨{#alternate-audio-tracks-in-the-playlist}

视频的播放列表可以为主视频内容指定不限数量的替代音轨。 例如，您可能希望向视频内容添加不同的语言，或者允许用户在播放内容时在设备上的不同轨道之间切换。

替代音轨或后期绑定音频允许用户在HTTP视频流（实时/线性和VOD）的多语言音轨之间切换，您不必为每个音轨修改、重复或重新打包视频。 您可以在资产初始打包之前或之后为视频资产提供多种语言跟踪。

>[!TIP]
>
>要使替代音频与主媒体的视频轨道混合，替代轨道的时间戳必须与主轨道中音频的时间戳匹配。

如果您使用替代音轨并加入广告，则以下要求适用：

* 如果主内容具有替代音轨，则广告必须至少具有一个纯音频流。
* 广告的纯音频流的每个区段持续时间必须等于广告视频流的区段持续时间。

主音轨包含在带有`default`标签的音轨集合中。 替代音频流的元数据包含在具有`TYPE=AUDIO`的`#EXT-X-MEDIA`标记的播放列表中。

例如，指定多个替代音频流的M3U8清单可能如下所示：

```
#EXTM3U
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 1",
 AUTOSELECT=YES,DEFAULT=YES
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 2",
 AUTOSELECT=NO,DEFAULT=NO,URI="alternate_audio_aac/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English",AUTOSELECT=YES,FORCED=NO,
 LANGUAGE="eng",URI="subtitles/eng/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English (Forced)",DEFAULT=YES,
 AUTOSELECT=YES,FORCED=YES,LANGUAGE="eng",URI="subtitles/eng_forced/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="Français",AUTOSELECT=YES,FORCED=NO,
 LANGUAGE="fra",URI="subtitles/fra/prog_index.m3u8"
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=263851,CODECS="mp4a.40.2, avc1.4d400d",
 RESOLUTION=416x234,AUDIO="bipbop_audio",SUBTITLES="subs" 
gear1/prog_index.m3u8
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=577610,CODECS="mp4a.40.2, avc1.4d401e",
 RESOLUTION=640x360,AUDIO="bipbop_audio",SUBTITLES="subs"
gear2/prog_index.m3u8
...
```

