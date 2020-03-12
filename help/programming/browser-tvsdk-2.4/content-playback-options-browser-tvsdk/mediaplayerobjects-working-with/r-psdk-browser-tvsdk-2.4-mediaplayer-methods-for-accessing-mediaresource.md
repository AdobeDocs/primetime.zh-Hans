---
description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
seo-description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
seo-title: 用于访问MediaResource信息的MediaPlayer属性
title: 用于访问MediaResource信息的MediaPlayer属性
uuid: d26f39d6-0a6b-4072-b99a-8767a511a846
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 用于访问MediaResource信息的MediaPlayer属性{#mediaplayer-attributes-to-access-mediaresource-information}

MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。

<table frame="all" colsep="1" rowsep="1" id="table_46225307CA5B4BB1869576E0B9141E38"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 用途 </th> 
   <th colname="2" class="entry"> 属性 </th> 
   <th colname="3" class="entry"> 说明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> 实时流 </td> 
   <td colname="2"> <span class="codeph"> live </span> </td> 
   <td colname="3"> 如果流是实时的，则为true;如果为VOD，则为false。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> 隐藏式字幕 </td> 
   <td colname="2"> <span class="codeph"> hasClosedCaptions </span> </td> 
   <td colname="3"> 如果隐藏式字幕轨道可用，则为True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks </span> </td> 
   <td colname="3"> 提供可用隐藏式字幕轨道列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedClosedCaptionsTrack </span> </td> 
   <td colname="3"> 检索使用selectClosedCaptionsTrack选择的隐藏字幕 <span class="codeph"> 轨道 </span>。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> 替代音频 </td> 
   <td colname="2"> <span class="codeph"> hasAlternateAudio </span> </td> 
   <td colname="3"> <p>如果流具有替代音轨，则为true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> audioTracks </span> </td> 
   <td colname="3"> 提供可用替代音轨的列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedAudioTrack </span> </td> 
   <td colname="3"> 
    <ph>
      检索当前选定的与selectAudioTrack一起选择的音 <span class="codeph"> 轨 </span>。 
    </ph> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> 定时元数据 </td> 
   <td colname="2"> <span class="codeph"> hasTimedMetadata </span> </td> 
   <td colname="3"> 如果流已关联定时元数据，则为true。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> timedMetadata </span> </td> 
   <td colname="3"> 提供与流关联的定时元数据对象的列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> 多个配置文件（位速率） </td> 
   <td colname="2" morerows="1"> <span class="codeph"> 配置文件 </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> 提供与此流关联的相关比特率配置文件的列表。 <p>注意： 您可以检索每个配置文件的位速率以及配置文件的高度和宽度。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 媒体资源 </td> 
   <td colname="2"> <span class="codeph"> 资源 </span> </td> 
   <td colname="3"> 返回与此项目关联的媒体资源。 </td> 
  </tr> 
 </tbody> 
</table>

