---
description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
title: 用于访问MediaResource信息的MediaPlayerItem方法
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# 用于访问MediaResource信息的MediaPlayerItem方法 {#mediaplayeritem-methods-for-accessing-mediaresource-information}

MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。

<table frame="all" colsep="1" rowsep="1" id="table_F6006A9167044AC087A6ECB20B8CCD5D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> 方法 </th> 
   <th colname="3" class="entry"> 描述 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="2"> <b>广告标记</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 列表&lt;string&gt; getAdTags() </span> </td> 
   <td colname="3"> 提供用于广告投放流程的广告标记列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>实时流</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布尔值isLive()； </span> </td> 
   <td colname="3"> 如果流是实时的，则为true；如果是VOD，则为false。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>受DRM保护</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布尔值isProtected()； </span> </td> 
   <td colname="3"> 如果流受DRM保护，则为True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 列表&lt;drmmetadatainfo&gt; getDRMMetadataInfos()； </span> </td> 
   <td colname="3"> 列出清单中发现的所有DRM元数据对象。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>隐藏式字幕</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasClosedCaptions()； </span> </td> 
   <td colname="3"> 如果隐藏式字幕轨道可用，则为True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 列表&lt;closedcaptionstrack&gt; getClosedCationsTracks()； </span> </td> 
   <td colname="3"> 提供可用隐藏式字幕跟踪的列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack get SelectedClosedCaptionsTrack()； </span> </td> 
   <td colname="3"> 检索当前的隐藏式字幕跟踪，选定为 <span class="codeph"> SelectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) </span> </td> 
   <td colname="3"> 将隐藏式字幕轨道设置为当前的隐藏式字幕轨道。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>备用音轨</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布尔值hasAlternateAudio()； </span> </td> 
   <td colname="3"> 如果流具有备用音轨，则为True。 <p>注意：主（默认）音轨也是备用音轨列表的一部分。 </p> <p>TVSDK for Android将主音频轨道视为备用音频轨道列表中的项目之一。 正因如此，唯一 <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> 返回false表示流完全没有音频。 如果内容只有一个音轨，则此方法返回true，并且 <span class="codeph"> MediaPlayerItem.getAudioTracks </span> 返回包含单个元素（默认音轨）的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 列表&lt;audiotrack&gt; getAudioTracks()； </span> </td> 
   <td colname="3"> 提供可用备用音频轨道的列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack()； </span> </td> 
   <td colname="3"> 检索与一起选择的音轨 <span class="codeph"> selectAudioTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack ( AudioTrack audioTrack ) </span> </td> 
   <td colname="3"> 选择一个要作为当前音轨的音轨。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>定时元数据</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasTimedMetadata()； </span> </td> 
   <td colname="3"> 如果流具有关联的定时元数据，则为True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 列表&lt;timedmetadata&gt; getTimedMetadata()； </span> </td> 
   <td colname="3"> 提供与流关联的定时元数据对象列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>多个配置文件（比特率）</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布尔值isDynamic()； </span> </td> 
   <td colname="3"> 如果流是多比特率(MBR)流，则为True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 列表&lt;profile&gt; getProfiles()； </span> </td> 
   <td colname="3"> 提供相关比特率配置文件的列表。 对于每个配置文件，您可以检索其比特率以及配置文件的高度和宽度。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 配置文件getSelectedProfile() </span> </td> 
   <td colname="3"> 检索当前选定的配置文件。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>特技游戏</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布尔值isTrickPlaySupported()； </span> </td> 
   <td colname="3"> 如果播放器支持快进、倒带和恢复，则为True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt; Float&gt; getAvailablePlaybackRates() </span> </td> 
   <td colname="3"> 提供特技播放功能上下文中的可用播放速率列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 浮动getSelectedPlaybackRate() </span> </td> 
   <td colname="3"> 检索当前选定的播放速率。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaPlayerItemConfig getConfig() </span> </td> 
   <td colname="3"> 返回 <span class="codeph"> MediaPlayerItemConfig </span> 与此项目关联的实例。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>媒体资源</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource()； </span> </td> 
   <td colname="3"> 返回与此项目关联的媒体资源。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> int getResourceId() </span> </td> 
   <td colname="3"> 返回与此项目关联的媒体标识符。 此ID在使用加载项时设置 <span class="codeph"> MediaPlayerItemLoader.load </span>. </td> 
  </tr> 
 </tbody> 
</table>
