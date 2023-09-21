---
description: MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。
title: 用于访问MediaResource信息的MediaPlayer属性
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 用于访问MediaResource信息的MediaPlayer属性{#mediaplayer-attributes-to-access-mediaresource-information}

MediaPlayerItem类中的方法允许您获取有关由加载的MediaResource表示的内容流的信息。

<table frame="all" colsep="1" rowsep="1" id="table_46225307CA5B4BB1869576E0B9141E38"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 用途 </th> 
   <th colname="2" class="entry"> 属性 </th> 
   <th colname="3" class="entry"> 描述 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> 实时流 </td> 
   <td colname="2"> <span class="codeph"> 实时 </span> </td> 
   <td colname="3"> 如果流是实时的，则为true；如果是VOD，则为false。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> 隐藏式字幕 </td> 
   <td colname="2"> <span class="codeph"> hasClosedCaptions </span> </td> 
   <td colname="3"> 如果隐藏式字幕轨道可用，则为True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks </span> </td> 
   <td colname="3"> 提供可用隐藏式字幕跟踪的列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedClosedCaptionsTrack </span> </td> 
   <td colname="3"> 检索与一起选择的隐藏式字幕轨道 <span class="codeph"> selectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> 备用音频 </td> 
   <td colname="2"> <span class="codeph"> hasAlternateAudio </span> </td> 
   <td colname="3"> <p>如果流具有备用音轨，则为True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> audioTracks </span> </td> 
   <td colname="3"> 提供可用备用音频轨道的列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedAudioTrack </span> </td> 
   <td colname="3"> 
    <pre>
      检索当前选择的音轨，该音轨用于 
     <span class="codeph"> selectAudioTrack </span>. 
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> 定时元数据 </td> 
   <td colname="2"> <span class="codeph"> hasTimedMetadata </span> </td> 
   <td colname="3"> 如果流具有关联的定时元数据，则为True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> timedMetadata </span> </td> 
   <td colname="3"> 提供与该流关联的定时元数据对象的列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> 多个配置文件（比特率） </td> 
   <td colname="2" morerows="1"> <span class="codeph"> 用户档案 </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> 提供与此流关联的关联比特率配置文件的列表。 <p>注意：您可以检索每个配置文件的比特率，以及配置文件的高度和宽度。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 媒体资源 </td> 
   <td colname="2"> <span class="codeph"> 资源 </span> </td> 
   <td colname="3"> 返回与此项目关联的媒体资源。 </td> 
  </tr> 
 </tbody> 
</table>
