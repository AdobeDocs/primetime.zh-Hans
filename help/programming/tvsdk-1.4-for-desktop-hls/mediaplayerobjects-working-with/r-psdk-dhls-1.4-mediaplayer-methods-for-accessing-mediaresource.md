---
description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
seo-description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
seo-title: 用于访问MediaResource信息的MediaPlayer方法
title: 用于访问MediaResource信息的MediaPlayer方法
uuid: c2d18f8e-4107-42bc-a975-9b881aadd27b
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661

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
   <td colname="1"> <b>实时流 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get isLive():Boolean; </span> </td> 
   <td colname="3"> <p>如果流是实时的，则为true;如果为VOD，则为false。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>DRM受保护</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get isProtected():Boolean; </span> </td> 
   <td colname="3"> <p>如果流受DRM保护，则为true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get drmMetadataInfos():矢量。&lt;DRMMetadataInfo&gt;; </span> </td> 
   <td colname="3"> <p>列出清单中发现的所有DRM元数据对象。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>隐藏式字幕</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get hasClosedCaptions():Boolean; </span> </td> 
   <td colname="3"> <p>如果隐藏式字幕轨道可用，则为True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get closedCaptionsTracks():Vector.&lt;ClosedCaptionsTrack&gt;; </span> </td> 
   <td colname="3"> <p>提供可用隐藏式字幕轨道列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get selectedClosedCaptionsTrack():ClosedCaptionsTrack </span> </td> 
   <td colname="3"> <p>检索使用SelectClosedCaptionsTrack选择的当前隐藏字幕 <span class="codeph"> 轨道 </span>。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack(closedCaptionsTrack:com.adobe.mediacore.info:ClosedCaptionsTrack) </span> </td> 
   <td colname="3"> <p>将隐藏式字幕轨道设置为当前隐藏式字幕轨道。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>替代音轨 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get hasAlternateAudio():Boolean; </span> </td> 
   <td colname="3"> <p>如果流具有替代音轨，则为true。 </p> <p>提示： 主音轨（默认）也是替代音轨列表的一部分。 </p> <p>桌面HLS的TVSDK认为主音轨是替代音轨列表中的项目之一。 因此，MediaPlayerItem.hasAlternateAudio返回false的唯一情况是当流完全没有音频 <span class="codeph"></span> 时。 如果内容只有一个音轨，则此方法返回true, <span class="codeph"> 并且AudioTracks返 </span> 回包含单个元素（默认音轨）的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get audioTracks():Vector.&lt;AudioTrack&gt;; </span> </td> 
   <td colname="3"> 提供可用替代音轨的列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get audioTracks():Vector.&lt;AudioTrack&gt;; </span> </td> 
   <td colname="3"> <p>提供可用替代音轨的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get selectedAudioTrack():AudioTrack; </span> </td> 
   <td colname="3"> <p>检索使用selectAudioTrack选择的音 <span class="codeph"> 轨 </span>。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack(audioTrack:AudioTrack) </span> </td> 
   <td colname="3"> <p>选择音轨作为当前音轨。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>定时元数据</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get hasTimedMetadata():Boolean; </span> </td> 
   <td colname="3"> <p>如果流已关联定时元数据，则为true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get timedMetadata():Vector.&lt;TimedMetadata&gt;; </span> </td> 
   <td colname="3"> <p>提供与流关联的定时元数据对象的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get isDynamic():Boolean; </span> </td> 
   <td colname="3"> <p>如果流是多位速率(MBR)流，则为true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get profiles():Vector.&lt;个人资料&gt;; </span> </td> 
   <td colname="3"> <p>提供关联的比特率配置文件列表。 对于每个配置文件，您可以检索其位速率以及配置文件的高度和宽度。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>特技播放 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get isTrickPlaySupported():Boolean; </span> </td> 
   <td colname="3"> <p>如果播放器支持快速前进、后退和恢复，则为true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get availablePlaybackRates():Vector.&lt;Number&gt; </span> </td> 
   <td colname="3"> <p>提供特技播放功能上下文中的可用播放速率列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>媒体播放器 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get player():MediaPlayer </span> </td> 
   <td colname="3"> <p>返回当前与此播放器关联的媒体播放器。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>媒体资源</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get resource():MediaResource; </span> </td> 
   <td colname="3"> <p>返回与此项目关联的媒体资源。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> 函数get resourceId():int </span> </td> 
   <td colname="3"> <p>返回与此项目关联的媒体标识符。 </p> </td> 
  </tr> 
 </tbody> 
</table>

