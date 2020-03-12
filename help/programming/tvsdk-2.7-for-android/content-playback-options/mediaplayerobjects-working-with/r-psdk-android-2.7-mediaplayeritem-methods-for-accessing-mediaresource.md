---
description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
seo-description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
seo-title: 用于访问MediaResource信息的MediaPlayerItem方法
title: 用于访问MediaResource信息的MediaPlayerItem方法
uuid: c6e77eb7-cefd-48aa-9373-2b44a96217a5
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 用于访问MediaResource信息的MediaPlayerItem方法 {#mediaplayeritem-methods-for-accessing-mediaresource-information}

MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。

<table frame="all" colsep="1" rowsep="1" id="table_F6006A9167044AC087A6ECB20B8CCD5D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> 方法 </th> 
   <th colname="3" class="entry"> 说明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="2"> <b>广告标记</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;String&gt; getAdTags() </span> </td> 
   <td colname="3"> 提供用于广告投放过程的广告标记列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>实时流</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isLive(); </span> </td> 
   <td colname="3"> 如果流是实时的，则为true;如果为VOD，则为false。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>DRM受保护</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isProtected(); </span> </td> 
   <td colname="3"> 如果流受DRM保护，则为true。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;DRMMetadataInfo&gt; getDRMMetadataInfos(); </span> </td> 
   <td colname="3"> 列出清单中发现的所有DRM元数据对象。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>隐藏式字幕</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasClosedCaptions(); </span> </td> 
   <td colname="3"> 如果隐藏式字幕轨道可用，则为True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;ClosedCaptionsTrack&gt; getClosedConsitionsTracks(); </span> </td> 
   <td colname="3"> 提供可用隐藏式字幕轨道列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack获取SelectedClosedCaptionsTrack(); </span> </td> 
   <td colname="3"> 检索使用SelectClosedCaptionsTrack选择的当前隐藏字幕 <span class="codeph"> 轨道 </span>。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack(ClosedCaptionsTrack closedCaptionsTrack) </span> </td> 
   <td colname="3"> 将隐藏式字幕轨道设置为当前隐藏式字幕轨道。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>替代音轨</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasAlternateAudio(); </span> </td> 
   <td colname="3"> 如果流具有替代音轨，则为true。 <p>注意： 主音轨（默认）也是替代音轨列表的一部分。 </p> <p>适用于Android的TVSDK将主音轨视为替代音轨列表中的项之一。 因此，MediaPlayerItem.hasAlternateAudio返回false的唯一情况是当流完全没有音频 <span class="codeph"></span> 时。 如果内容只有一个音轨，则此方法返回true, <span class="codeph"></span> MediaPlayerItem.getAudioTracks返回一个包含单个元素（默认音轨）的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;AudioTrack&gt; getAudioTracks(); </span> </td> 
   <td colname="3"> 提供可用替代音轨的列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack(); </span> </td> 
   <td colname="3"> 检索使用selectAudioTrack选择的音 <span class="codeph"> 轨 </span>。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack(AudioTrack audioTrack) </span> </td> 
   <td colname="3"> 选择音轨作为当前音轨。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>定时元数据</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasTimedMetadata(); </span> </td> 
   <td colname="3"> 如果流已关联定时元数据，则为true。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;TimedMetadata&gt; getTimedMetadata(); </span> </td> 
   <td colname="3"> 提供与流关联的定时元数据对象的列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>多个配置文件（位速率）</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isDynamic(); </span> </td> 
   <td colname="3"> 如果流是多位速率(MBR)流，则为true。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;Profile&gt; getProfiles(); </span> </td> 
   <td colname="3"> 提供关联的比特率配置文件列表。 对于每个配置文件，您可以检索其位速率以及配置文件的高度和宽度。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 配置文件getSelectedProfile() </span> </td> 
   <td colname="3"> 检索当前选定的配置文件。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>特技播放</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isTrickPlaySupported(); </span> </td> 
   <td colname="3"> 如果播放器支持快速前进、后退和恢复，则为true。 </td> 
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
   <td colname="3"> 返回与 <span class="codeph"> 此项目关 </span> 联的MediaPlayerItemConfig实例。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>媒体资源</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource(); </span> </td> 
   <td colname="3"> 返回与此项目关联的媒体资源。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> int getResourceId() </span> </td> 
   <td colname="3"> 返回与此项目关联的媒体标识符。 使用MediaPlayerItemLoader.load加载项目时，将设 <span class="codeph"> 置此ID </span>。 </td> 
  </tr> 
 </tbody> 
</table>
