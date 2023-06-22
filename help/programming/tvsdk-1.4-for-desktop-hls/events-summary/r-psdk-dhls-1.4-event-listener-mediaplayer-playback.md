---
description: 您的应用程序可以通过侦听由TVSDK调度的事件来监控播放器中的活动和播放器的更改状态。
title: 播放事件
exl-id: 9fb77b57-be6c-4dab-b779-d8c606938e46
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# 播放事件 {#playback-events}

您的应用程序可以通过侦听由TVSDK调度的事件来监控播放器中的活动和播放器的更改状态。

TVSDK会在媒体播放操作（例如开始播放的视频）发生时调度播放事件。 要收到有关所有播放相关事件的通知，请将监听器注册到 `MediaPlayer` 对象。

<table frame="all" colsep="1" rowsep="1" id="table_922EEA3DE0BD47BA982E11F890CA0A6B"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 事件 </th> 
   <th colname="2" class="entry"> 含义 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>播放</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_SELECTED" format="html" scope="external"> RATE_SELECTED</a> </td> 
   <td colname="2"> 用户或TVSDK已选择新的播放速率，例如快进、倒带或以正常速度继续播放。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_PLAYING" format="html" scope="external"> RATE_PLAYING</a> </td> 
   <td colname="2"> 屏幕上将显示新的播放速率。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> TimeChangeEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html#TIME_CHANGED" format="html" scope="external"> TIME_CHANGED</a> </td> 
   <td colname="2"> 媒体的当前播放头位置已更改。 当当前时间发生变化时，定期发送，每250毫秒或更长时间。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>媒体播放器</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerStatus ChangeEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html#STATUS_CHANGED" format="html" scope="external"> STATUS_CHANGED</a> </td> 
   <td colname="2"> 媒体播放器的状态已更改。 您的应用程序应处理此事件回调中的错误。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ProfileEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html#PROFILE_CHANGED" format="html" scope="external"> 配置文件已更改</a> </td> 
   <td colname="2">媒体播放器的当前配置文件已更改。 使用 <span class="codeph"> ProfileEvent.profile</span> 属性以获取正在播放的新配置文件。 使用 <span class="codeph"> 时间</span> 属性，用于获取此事件发生时的时间。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>MediaplayerItem</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_CREATED" format="html" scope="external"> ITEM_CREATE</a> </td> 
   <td colname="2">A <span class="codeph"> MediaPlayerItem</span> 已创建。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_UPDATED" format="html" scope="external"> 已更新项目</a> </td> 
   <td colname="2">在以下任一情况下，媒体播放器已成功更新媒体： 
    <ul id="ul_E4D1A1D468544C3B9F8046E9B68A956D"> 
     <li id="li_35A2A417BF924E039D9CB36CFBCDFEB6">当实时资产发生清单刷新时。 </li> 
     <li id="li_E7AB380C212B4011B07C3B313282681C">当VOD或实时资产具有隐藏式字幕并且首次发现隐藏式字幕跟踪的活动时。 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>字幕和音频</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#CAPTION_UPDATED" format="html" scope="external"> 题注已更新</a> </td> 
   <td colname="2">在媒体流中检测到新的隐藏式字幕轨道，并且 <span class="codeph"> closedCaptionsTracks</span> 已更新收藏集。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>清单和时间线</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="0"> 
   <td colname="1">时间线事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED" format="html" scope="external"> 时间线已更新</a> </td> 
   <td colname="2">媒体播放器已添加或删除广告，因此它拥有更新的时间轴。 <p>为实时资源刷新的清单并从时间轴中删除了旧的广告时间或发现了新的广告机会（提示点）。 媒体播放器会尝试解析任何新广告，并将其放在时间轴上。 </p> <p> 使用此事件检查时间线是否有任何更新（播放期间VOD不会更改）。 然后，您可以使用检索时间轴 <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html#timeline" format="html" scope="external"> MediaPlayer.timeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
