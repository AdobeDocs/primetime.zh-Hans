---
description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
title: 用于访问MediaResource信息的MediaPlayer方法
exl-id: 8849411a-e94b-43a9-9fa1-143725264304
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 用于访问MediaResource信息的MediaPlayer方法{#mediaplayer-methods-for-accessing-mediaresource-information}

MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。

<table frame="all" colsep="1" rowsep="1" id="table_77B55D506FE24326A03D97AA087231FF"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> 方法 </th> 
   <th colname="3" class="entry"> 描述 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <b>广告标记</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 列表&lt;string&gt; getAdTags() </span> </td> 
   <td colname="3"> <p>提供用于广告投放流程的广告标记列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>实时流</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布尔值isLive()； </span> </td> 
   <td colname="3"> <p>如果流是实时的，则为true；如果是VOD，则为false。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>受DRM保护</b> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布尔值isProtected()； </span> </td> 
   <td colname="3"> <p>如果流受DRM保护，则为True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 列表&lt;drmmetadatainfo&gt; getDRMMetadataInfos()； </span> </td> 
   <td colname="3"> <p>列出清单中发现的所有DRM元数据对象。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>隐藏字幕</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布尔型hasClosedCaptions()； </span> </td> 
   <td colname="3"> <p>如果隐藏式字幕跟踪可用，则为True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 列表&lt;closedcaptionstrack&gt; getClosedCationsTracks()； </span> </td> 
   <td colname="3"> <p>提供可用隐藏式字幕字幕的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack get SelectedClosedCaptionsTrack()； </span> </td> 
   <td colname="3"> <p>检索当前选定的隐藏式字幕跟踪 <span class="codeph"> SelectClosedCaptionsTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) </span> </td> 
   <td colname="3"> <p>将隐藏式字幕轨迹设置为当前的隐藏式字幕轨迹。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>备用音轨</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布尔值hasAlternateAudio()； </span> </td> 
   <td colname="3"> <p>如果流具有备用音轨，则为True。 </p> <p>提示：主（默认）音轨也是备用音轨列表的一部分。 </p> <p>适用于Android的TVSDK将主音频轨道视为备用音频轨道列表中的项目之一。 正因为如此，只有这样 <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> 如果流完全没有音频，则返回false。 如果内容只有一个音轨，则此方法返回true，并且 <span class="codeph"> MediaPlayerItem.getAudioTracks </span> 返回带有单个元素（默认音轨）的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 列表&lt;audiotrack&gt; getAudioTracks()； </span> </td> 
   <td colname="3"> 提供可用备用音轨的列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 列表&lt;audiotrack&gt; getAudioTracks()； </span> </td> 
   <td colname="3"> <p>提供可用备用音轨的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack()； </span> </td> 
   <td colname="3"> <p>检索选择的音轨，并显示 <span class="codeph"> selectAudioTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack ( AudioTrack audioTrack ) </span> </td> 
   <td colname="3"> <p>选择一个音轨作为当前音轨。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>定时元数据</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布尔型hasTimedMetadata()； </span> </td> 
   <td colname="3"> <p>如果流具有关联的定时元数据，则为True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 列表&lt;timedmetadata&gt; getTimedMetadata()； </span> </td> 
   <td colname="3"> <p>提供与流关联的定时元数据对象列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布尔值isDynamic()； </span> </td> 
   <td colname="3"> <p>如果流是多比特率(MBR)流，则为True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 列表&lt;profile&gt; getProfiles()； </span> </td> 
   <td colname="3"> <p>提供相关比特率配置文件的列表。 对于每个配置文件，您可以检索其比特率以及配置文件的高度和宽度。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>特技游戏</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布尔值isTrickPlaySupported()； </span> </td> 
   <td colname="3"> <p>如果播放器支持快进、倒带和恢复，则为True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt; Float&gt; getAvailablePlaybackRates </span> </td> 
   <td colname="3"> <p>提供特技播放功能上下文中的可用播放速率列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>媒体资源</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource()； </span> </td> 
   <td colname="3"> <p>返回与此项目关联的媒体资源。 </p> </td> 
  </tr> 
 </tbody> 
</table>
