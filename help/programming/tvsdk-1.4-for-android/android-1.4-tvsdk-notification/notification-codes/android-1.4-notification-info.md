---
description: 此表提供有关INFO的详细信息。 键入通知。
title: INFO通知代码
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 4%

---

# INFO通知代码{#info-notification-codes}

此表提供有关INFO的详细信息。 键入通知。

<!--<a id="section_ED4302E363AE48CBA2C3E0B71AE612D8"></a>-->

大多数信息性通知包含相关元数据，例如，下载失败的资源的URL。 某些通知包含元数据，用于指定问题出现在主视频内容、备用音频内容还是广告中。

<table frame="all" colsep="1" rowsep="1" id="table_503463046E764A87B10EB5D8B294EB23"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 代码 </th> 
   <th colname="2" class="entry"> 名称 </th> 
   <th colname="3" class="entry"> 内部通知 </th> 
   <th colname="4" class="entry"> 元数据键 </th> 
   <th colname="5" class="entry"> 评论 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>播放</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_START </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"> 无 </td> 
   <td colname="5"> 已开始播放。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300001 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_COMPLETE </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"> 无 </td> 
   <td colname="5"> 播放已完成。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300002 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_START </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 搜寻时间</span> </td> 
   <td colname="5"> 已启动搜寻操作。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_COMPLETE </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 搜寻时间</span> </td> 
   <td colname="5"> 搜寻操作已完成。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300004 </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_CHANGE </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"> <span class="codeph"> CONTENT_ID</span> <span class="codeph"> CURRENT_MEDIA_TIME</span> </td> 
   <td colname="5"> 当前播放时间已超过主内容和替代内容之间的边界。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005 </span> </td> 
   <td colname="2"><span class="codeph"> player_STATE_CHANGE </span> </td> 
   <td colname="3"> <p>任何错误通知。 </p> </td> 
   <td colname="4"><span class="codeph"> 状态 </span> </td> 
   <td colname="5"> 播放器状态已更改。 当状态为ERROR时，内部通知是触发切换到ERROR状态的错误通知对象。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300006 </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_MARKER </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID CURRENT_MEDIA_TIME </span> </td> 
   <td colname="5"> 已收到内容标记。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300100 </span> </td> 
   <td colname="2"><span class="codeph"> LOAD_INFO_AVAILABLE </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"> <span class="codeph"> FRAGMENT_URL</span> <span class="codeph"> FRAGMENT_SIZE</span> <span class="codeph"> FRAGMENT_DOWNLOAD_DURATION</span> <span class="codeph"> PERIOD_INDEX</span> </td> 
   <td colname="5"> 提供与视频区段下载方式相关的信息。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300101 </span> </td> 
   <td colname="2"><span class="codeph"> VIDEO_SIZE_CHANGED </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"> <span class="codeph"> 高度</span> <p><span class="codeph"> 宽度</span> </p> </td> 
   <td colname="5"> 视频播放窗口的大小已更改。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>自适应比特率(ABR)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 302000 </span> </td> 
   <td colname="2"><span class="codeph"> BITRATE_CHANGE </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"><span class="codeph"> BITRATE </span><span class="codeph"> CURRENT_MEDIA_TIME </span> </td> 
   <td colname="5"> 视频的比特率已更改。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>广告处理</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303000 </span> </td> 
   <td colname="2"><span class="codeph"> 时间线更改 </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID </span><span class="codeph"> PERIOD_INDEX </span> </td> 
   <td colname="5"> 时间轴已更改（例如，添加或删除了替代内容）。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_PLACEMENT_COMPLETE </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"> <span class="codeph"> PROPOSED_AD_BREAK</span> <span class="codeph"> ACCEPTED_AD_BREAK</span> </td> 
   <td colname="5"> 提议的广告时间已被接受 <code>primetime-sdk-name</code> 并将其完全或部分放置在播放时间轴上。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303002 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_START </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"><span class="codeph"> AD_BREAK </span> </td> 
   <td colname="5"> 特定广告时间的播放已开始。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_COMPLETE </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"><span class="codeph"> AD_BREAK </span> </td> 
   <td colname="5"> 特定广告时间的播放已完成。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303004 </span> </td> 
   <td colname="2"><span class="codeph"> AD_START </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> 广告</span> </p> </td> 
   <td colname="5"> 特定广告的播放已开始。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_COMPLETE </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> 广告</span> </p> </td> 
   <td colname="5"> 特定广告的播放已完成。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303006 </span> </td> 
   <td colname="2"><span class="codeph"> AD_PROGRESS </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> 广告</span> </p> <span class="codeph"> 进度</span> </td> 
   <td colname="5"> 特定广告的播放已达到该特定广告的某个百分比。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303007 </span> </td> 
   <td colname="2"><span class="codeph"> TIMED_METADATA_ADD </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"> <span class="codeph"> 类型</span> <p><span class="codeph"> ID</span> </p> <span class="codeph"> 名称</span> <p><span class="codeph"> 时间</span> </p> </td> 
   <td colname="5"> 在清单中发现了新的定时元数据。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303008 </span> </td> 
   <td colname="2"><span class="codeph"> AD_CLICK </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> 广告</span> </p> <span class="codeph"> AD_CLICK</span> </td> 
   <td colname="5"> 返回有关用户点击的广告的信息。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303009</span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_SKIPPED</span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> 广告</span> </p> <span class="codeph"> AD_CLICK</span> </td> 
   <td colname="5"> 已跳过广告时间。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname=""><b>延迟绑定音频(LBA)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 304000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"><span class="codeph"> TRACK_ID </span><span class="codeph"> CURRENT_MEDIA_TIME </span> </td> 
   <td colname="5"> 音轨已更改。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 305000 </span> </td> 
   <td colname="2"><span class="codeph"> DRM_METADATA_AVAILABLE </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"><span class="codeph"> PREFETCH_TIMESTAMP </span> </td> 
   <td colname="5"> 有新的DRM数据可用。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>通用</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 399999 </span> </td> 
   <td colname="2"><span class="codeph"> GENER_INFO </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"> <p>无 </p> </td> 
   <td colname="5"> <p>标记一般信息事件。 不是由TVSDK实际颁发的。 它只是对应于TVSDK信息事件的数值代码范围的结束标记。 </p> </td> 
  </tr> 
 </tbody> 
</table>
