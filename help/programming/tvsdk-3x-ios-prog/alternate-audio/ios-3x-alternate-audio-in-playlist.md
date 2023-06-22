---
description: 备用或延迟绑定的音频允许您在视频曲目的可用音频曲目之间切换。 通过这种方式，用户可以在播放视频时选择语言跟踪。
title: 播放列表中的备用音轨
exl-id: d8d8c122-5837-4f0e-934f-a3d6e1b037c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 播放列表中的备用音轨 {#section_BC8C1C74A5A24A8CA68C1E7E721EE742}

视频的播放列表可以为主视频内容指定无限数量的替代音频轨道。 例如，您可能希望向视频内容添加不同的语言，或者允许用户在播放内容时在其设备上的不同曲目之间切换。

备用音频轨道（或后期捆绑音频）允许用户在HTTP视频流的多个语言轨道（实时/线性和VOD）之间进行切换，您无需为每个音频轨道修改、复制或重新打包视频。 您可以在视频资产初始打包之前或之后，为该资产提供多个语言跟踪。

>[!TIP]
>
>对于要与主媒体的视频轨道混合的替代音频，替代轨道的时间戳必须与主轨道中音频的时间戳匹配。

如果您使用备用音轨并合并广告，则以下要求适用：

* 如果主内容具有替代的音频轨道，则广告必须具有至少一个纯音频流。
* 广告的纯音频流的每个区段持续时间必须等于广告视频流的区段持续时间。

主音轨通过包含在音轨集合中 `default` 标签。 替代音频流的元数据包括在的播放列表中 `#EXT-X-MEDIA` 标记方式 `TYPE=AUDIO`.

例如，指定多个备用音频流的M3U8清单可能如下所示：

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
