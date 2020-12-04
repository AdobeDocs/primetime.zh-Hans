---
description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
seo-description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
seo-title: 用于访问MediaResource信息的MediaPlayer方法
title: 用于访问MediaResource信息的MediaPlayer方法
uuid: 5d83491c-6577-46fe-98af-83f0fde7a7d0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---


# 用于访问MediaResource信息的MediaPlayer方法{#mediaplayer-methods-for-accessing-mediaresource-information}

MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。

<table frame="all" colsep="1" rowsep="1" id="table_77B55D506FE24326A03D97AA087231FF"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> 方法 </th> 
   <th colname="3" class="entry"> 说明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <b>广告标记</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;string&gt; ListgetAdTags()  </span> </td> 
   <td colname="3"> <p>提供用于广告投放流程的广告标签的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>实时流</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isLive();  </span> </td> 
   <td colname="3"> <p>如果流是实时的，则为true;如果为VOD，则为false。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>DRM受保护</b> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isProtected();  </span> </td> 
   <td colname="3"> <p>如果流受DRM保护，则为true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;drmmetadatainfo&gt; ListgetDRMMetadataInfos();  </span> </td> 
   <td colname="3"> <p>列表清单中发现的所有DRM元数据对象。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>隐藏式字幕</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasClosedCaptions();  </span> </td> 
   <td colname="3"> <p>如果隐藏式字幕轨道可用，则为true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;closedcaptionstrack&gt; ListgetClosedActionsTracks();  </span> </td> 
   <td colname="3"> <p>提供可用隐藏字幕轨道的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack获取SelectedClosedCaptionsTrack();  </span> </td> 
   <td colname="3"> <p>检索使用<span class="codeph"> SelectClosedCaptionsTrack </span>选择的当前隐藏字幕轨道。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack(ClosedCaptionsTrack closedCaptionsTrack)  </span> </td> 
   <td colname="3"> <p>将隐藏字幕轨道设置为当前隐藏字幕轨道。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>替代音轨</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasAlternateAudio();  </span> </td> 
   <td colname="3"> <p>如果流具有替代音轨，则为true。 </p> <p>提示： 主音轨（默认）也是替代音轨列表的一部分。 </p> <p>适用于Android的TVSDK将主音轨视为备选音轨列表中的项目之一。 因此，<span class="codeph"> MediaPlayerItem.hasAlternateAudio </span>返回false的唯一情况是当流完全没有音频时。 如果内容只有一个音轨，则此方法返回true，而<span class="codeph"> MediaPlayerItem.getAudioTracks </span>返回具有单个元素（默认音轨）的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;audiotrack&gt; ListgetAudioTracks();  </span> </td> 
   <td colname="3"> 提供可用备用音轨的列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;audiotrack&gt; ListgetAudioTracks();  </span> </td> 
   <td colname="3"> <p>提供可用备用音轨的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack();  </span> </td> 
   <td colname="3"> <p>检索使用<span class="codeph"> selectAudioTrack </span>选择的音轨。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack(AudioTrack audioTrack)  </span> </td> 
   <td colname="3"> <p>选择一个音轨作为当前音轨。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>定时元数据</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasTimedMetadata();  </span> </td> 
   <td colname="3"> <p>如果流具有关联的定时元数据，则为true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;timedmetadata&gt; ListgetTimedMetadata();  </span> </td> 
   <td colname="3"> <p>提供与流关联的定时元数据对象的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isDynamic();  </span> </td> 
   <td colname="3"> <p>如果流是多比特率(MBR)流，则为true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ListgetProfiles(&lt;profile&gt; );  </span> </td> 
   <td colname="3"> <p>提供相关比特率列表用户档案。 对于每个用户档案，您可以检索其比特率以及用户档案的高度和宽度。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>技巧游戏</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isTrickPlaySupported();  </span> </td> 
   <td colname="3"> <p>如果播放器支持快速前进、后退和恢复，则为true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ListgetAvailablePlaybackRates &lt; Float=""&gt;   </span> </td> 
   <td colname="3"> <p>在特技播放功能的上下文中提供可用播放速率的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>媒体资源</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource();  </span> </td> 
   <td colname="3"> <p>返回与此项目关联的媒体资源。 </p> </td> 
  </tr> 
 </tbody> 
</table>

