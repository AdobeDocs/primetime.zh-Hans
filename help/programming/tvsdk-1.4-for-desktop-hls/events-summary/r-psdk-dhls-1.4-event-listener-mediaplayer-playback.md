---
description: 您的应用程序可以监听TVSDK调度的活动，监视播放器中的事件和播放器的更改状态。
title: 播放事件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# 播放事件{#playback-events}

您的应用程序可以监听TVSDK调度的活动，监视播放器中的事件和播放器的更改状态。

TVSDK在进行媒体播放操作（如视频开始播放）时调度播放事件。 要获得有关所有播放相关事件的通知，请向`MediaPlayer`对象注册以下事件的监听器。

<table frame="all" colsep="1" rowsep="1" id="table_922EEA3DE0BD47BA982E11F890CA0A6B"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 事件 </th> 
   <th colname="2" class="entry"> 意义 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>播放</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_SELECTED" format="html" scope="external"> RATE_SELECTED</a> </td> 
   <td colname="2"> 用户或TVSDK选择了新的播放速率，如快速前进、后退或以正常速度继续播放。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_PLAYING" format="html" scope="external"> RATE_PLAYING</a> </td> 
   <td colname="2"> 屏幕上会显示新的播放率。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> TimeChangeEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html#TIME_CHANGED" format="html" scope="external"> TIME_CHANGED</a> </td> 
   <td colname="2"> 媒体的当前播放头位置已更改。 当当前时间发生更改时，每250毫秒或更长时间定期调度一次。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Media Player</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerStatus ChangeEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html#STATUS_CHANGED" format="html" scope="external"> STATUS_CHANGED</a> </td> 
   <td colname="2"> 媒体播放器的状态已更改。 您的应用程序应处理此事件回调中的错误。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ProfileEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html#PROFILE_CHANGED" format="html" scope="external"> 用户档案_CHANGED</a> </td> 
   <td colname="2">媒体播放器的当前用户档案已更改。 使用<span class="codeph"> ProfileEvent.用户档案</span>属性获取正在播放的新用户档案。 使用<span class="codeph"> time</span>属性可获取发生此事件的时间。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>MediaplayerItem</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_CREATED" format="html" scope="external"> ITEM_CREATED</a> </td> 
   <td colname="2">已创建<span class="codeph"> MediaPlayerItem</span>。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_UPDATED" format="html" scope="external"> ITEM_UPDATED</a> </td> 
   <td colname="2">在以下任一情况下，媒体播放器已成功更新媒体： 
    <ul id="ul_E4D1A1D468544C3B9F8046E9B68A956D"> 
     <li id="li_35A2A417BF924E039D9CB36CFBCDFEB6">当实时资产发生清单刷新时。 </li> 
     <li id="li_E7AB380C212B4011B07C3B313282681C">当VOD或实时资产包含隐藏式字幕并且首次为隐藏式字幕轨道发现活动时。 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>字幕和音频</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#CAPTION_UPDATED" format="html" scope="external"> CAPTION_UPDATED</a> </td> 
   <td colname="2">在媒体流中检测到新的隐藏字幕轨道，并更新了<span class="codeph"> closedCaptionsTracks</span>集合。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>清单和时间轴</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="0"> 
   <td colname="1">TimelineEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED" format="html" scope="external"> TIMELINE_UPDATED</a> </td> 
   <td colname="2">媒体播放器已添加或删除广告，因此具有更新的时间轴。 <p>已从时间轴中删除为实时资产刷新的清单和旧的广告分段，或发现新的广告机会（提示点）。 媒体播放器会尝试解析任何新广告并将其放置在时间轴上。 </p> <p> 使用此事件检查时间轴是否有任何更新（播放期间VOD没有更改）。 然后，可以使用<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html#timeline" format="html" scope="external"> MediaPlayer.timeline</a>检索时间轴。 </p> </td> 
  </tr> 
 </tbody> 
</table>

