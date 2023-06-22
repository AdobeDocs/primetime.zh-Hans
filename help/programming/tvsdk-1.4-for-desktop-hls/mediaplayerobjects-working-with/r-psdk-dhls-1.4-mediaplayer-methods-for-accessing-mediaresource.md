---
description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
title: 用于访问MediaResource信息的MediaPlayer方法
exl-id: 74e453d6-233e-4146-9f63-ab6919a4ba39
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '449'
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
   <td colname="1"> <b>实时流 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get isLive()：Boolean； </span> </td> 
   <td colname="3"> <p>如果流是实时的，则为true；如果是VOD，则为false。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>受DRM保护</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get isProtected()：Boolean； </span> </td> 
   <td colname="3"> <p>如果流受DRM保护，则为True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数获取drmMetadataInfos()： Vector。&lt;drmmetadatainfo&gt;； </span> </td> 
   <td colname="3"> <p>列出清单中发现的所有DRM元数据对象。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>隐藏字幕</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get hasClosedCaptions()：Boolean； </span> </td> 
   <td colname="3"> <p>如果隐藏式字幕跟踪可用，则为True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get closedCaptionsTracks()：Vector.&lt;closedcaptionstrack&gt;； </span> </td> 
   <td colname="3"> <p>提供可用隐藏式字幕字幕的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get selectedClosedCaptionsTrack()：ClosedCaptionsTrack </span> </td> 
   <td colname="3"> <p>检索当前选定的隐藏式字幕跟踪 <span class="codeph"> SelectClosedCaptionsTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack (closedCaptionsTrack： com.adobe.mediacore.info：ClosedCaptionsTrack ) </span> </td> 
   <td colname="3"> <p>将隐藏式字幕轨迹设置为当前的隐藏式字幕轨迹。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>备用音轨 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get hasAlternateAudio()：Boolean； </span> </td> 
   <td colname="3"> <p>如果流具有备用音轨，则为True。 </p> <p>提示：主（默认）音轨也是备用音轨列表的一部分。 </p> <p>TVSDK for Desktop HLS将主音频轨道视为备用音频轨道列表中的项目之一。 正因为如此，只有这样 <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> 如果流完全没有音频，则返回false。 如果内容只有一个音轨，则此方法返回true，并且 <span class="codeph"> 获取音轨 </span> 返回带有单个元素（默认音轨）的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get audioTracks()：Vector.&lt;audiotrack&gt;； </span> </td> 
   <td colname="3"> 提供可用备用音轨的列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get audioTracks()：Vector.&lt;audiotrack&gt;； </span> </td> 
   <td colname="3"> <p>提供可用备用音轨的列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get selectedAudioTrack()：AudioTrack； </span> </td> 
   <td colname="3"> <p>检索选择的音轨，并显示 <span class="codeph"> selectAudioTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack(audioTrack： AudioTrack ) </span> </td> 
   <td colname="3"> <p>选择一个音轨作为当前音轨。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>定时元数据</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get hasTimedMetadata()：Boolean； </span> </td> 
   <td colname="3"> <p>如果流具有关联的定时元数据，则为True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get timedMetadata()：Vector.&lt;timedmetadata&gt;； </span> </td> 
   <td colname="3"> <p>提供与流关联的定时元数据对象列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get isDynamic()：Boolean； </span> </td> 
   <td colname="3"> <p>如果流是多比特率(MBR)流，则为True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get profiles()：Vector。&lt;profile&gt;； </span> </td> 
   <td colname="3"> <p>提供相关比特率配置文件的列表。 对于每个配置文件，您可以检索其比特率以及配置文件的高度和宽度。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>特技游戏 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get isTrickPlaySupported()：Boolean； </span> </td> 
   <td colname="3"> <p>如果播放器支持快进、倒带和恢复，则为True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get availablePlaybackRates()：Vector.&lt;Number&gt; </span> </td> 
   <td colname="3"> <p>提供特技播放功能上下文中的可用播放速率列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>媒体播放器 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数获取播放器()：MediaPlayer </span> </td> 
   <td colname="3"> <p>返回当前与此播放器关联的媒体播放器。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>媒体资源</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函数get resource()：MediaResource； </span> </td> 
   <td colname="3"> <p>返回与此项目关联的媒体资源。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> 函数get resourceId()：int </span> </td> 
   <td colname="3"> <p>返回与此项目关联的媒体标识符。 </p> </td> 
  </tr> 
 </tbody> 
</table>
