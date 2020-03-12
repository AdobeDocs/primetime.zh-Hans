---
description: 您的应用程序可以监听TVSDK调度的事件，以监视播放器中的活动和播放器的更改状态。
seo-description: 您的应用程序可以监听TVSDK调度的事件，以监视播放器中的活动和播放器的更改状态。
seo-title: 播放事件
title: 播放事件
uuid: 6d6491d7-cf25-4130-8388-68b8c028bb71
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 播放事件 {#playback-events}

您的应用程序可以监听TVSDK调度的事件，以监视播放器中的活动和播放器的更改状态。

TVSDK在进行媒体播放操作（如视频开始播放）时调度播放事件。 要获得有关所有播放相关事件的通知，请向以下事件的对象 `MediaPlayer` 注册监听器。

<table frame="all" colsep="1" rowsep="1" id="table_922EEA3DE0BD47BA982E11F890CA0A6B"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 活动 </th> 
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
   <td colname="2"> 用户或TVSDK已选择新的播放速率，如以正常速度快进、后退或继续播放。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_PLAYING" format="html" scope="external"> RATE_PLAYING</a> </td> 
   <td colname="2"> 屏幕上会显示新的播放速率。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> TimeChangeEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html#TIME_CHANGED" format="html" scope="external"> TIME_CHANGED</a> </td> 
   <td colname="2"> 媒体的当前播放头位置已更改。 在当前时间发生更改时定期分派，每隔250毫秒或更长时间。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Media Player</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerStatus ChangeEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html#STATUS_CHANGED" format="html" scope="external"> STATUS_CHANGED</a> </td> 
   <td colname="2"> 媒体播放器的状态已更改。 应用程序应处理此事件回调中的错误。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">个人资料——事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html#PROFILE_CHANGED" format="html" scope="external"> PROFILE_CHANGED</a> </td> 
   <td colname="2">媒体播放器的当前配置文件已更改。 使用 <span class="codeph"> ProfileEvent.profile</span> 属性获取正在播放的新配置文件。 使用 <span class="codeph"> time</span> 属性获取发生此事件的时间。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>MediaplayerItem</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_CREATED" format="html" scope="external"> ITEM_CREATED</a> </td> 
   <td colname="2">已 <span class="codeph"> 创建MediaPlayerItem</span> 。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_UPDATED" format="html" scope="external"> ITEM_UPDATED</a> </td> 
   <td colname="2">在以下任一情况下，媒体播放器已成功更新媒体： 
    <ul id="ul_E4D1A1D468544C3B9F8046E9B68A956D"> 
     <li id="li_35A2A417BF924E039D9CB36CFBCDFEB6">当实时资产发生清单刷新时。 </li> 
     <li id="li_E7AB380C212B4011B07C3B313282681C">当VOD或实时资产具有关闭的字幕时，并且首次为关闭的字幕轨道发现活动时。 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>字幕和音频</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#CAPTION_UPDATED" format="html" scope="external"> CAPTION_UPDATED</a> </td> 
   <td colname="2">在媒体流中检测到新的隐藏字幕轨道，并且 <span class="codeph"></span> closedCaptionsTracks集合已更新。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>清单和时间轴</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="0"> 
   <td colname="1">TimelineEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED" format="html" scope="external"> TIMELINE_UPDATED</a> </td> 
   <td colname="2">媒体播放器已添加或删除广告，因此它具有更新的时间轴。 <p>已从时间轴中删除为实时资产刷新的清单和旧广告分段，或发现新的广告机会（提示点）。 媒体播放器会尝试解析任何新广告并将其放在时间轴上。 </p> <p> 使用此事件检查时间轴是否有任何更新（播放期间VOD不会更改）。 然后，您可以使用MediaPlayer.timeline检索 <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html#timeline" format="html" scope="external"> 时间轴</a>。 </p> </td> 
  </tr> 
 </tbody> 
</table>

