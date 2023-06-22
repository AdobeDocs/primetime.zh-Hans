---
description: TVSDK会在媒体播放操作（例如开始播放的视频）发生时调度播放事件。
title: 播放事件
exl-id: 675dd444-d58c-4316-9d62-b64e6433b650
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# 播放事件{#playback-events}

TVSDK会在媒体播放操作（例如开始播放的视频）发生时调度播放事件。

要收到有关所有播放相关事件的通知，请注册以下实施 `MediaPlayer.PlaybackEventListener`，包括以下事件回调。

<table frame="all" colsep="1" rowsep="1"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 事件 </th> 
   <th colname="2" class="entry"> 含义 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="col1"><b>播放</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPlayComplete%28%29" format="html" scope="external"> onPlayComplete</a> </td> 
   <td colname="2"> 已达到媒体源的结尾。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPlayStart%28%29" format="html" scope="external"> onPlaystart</a> </td> 
   <td colname="2"> 已开始播放媒体源。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRateSelected%28float%29" format="html" scope="external"> onRateSelected</a> （浮动比率） </td> 
   <td colname="2"> 用户或TVSDK已选择新的播放速率，例如快进、倒带或以正常速度继续播放。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRatePlaying%28float%29" format="html" scope="external"> onRatePlaying</a> （浮动比率） </td> 
   <td colname="2"> 屏幕上将显示新的播放速率。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>媒体</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPrepared%28%29" format="html" scope="external"> onPrepared</a> </td> 
   <td colname="2"> 媒体播放器已成功准备媒体。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onSizeAvailable%28long,%20long%29" format="html" scope="external"> onSizeAvailable</a> （长高，长宽） </td> 
   <td colname="2"> 介质的大小可用。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>媒体播放器</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onStateChanged%28com.adobe.mediacore.MediaPlayer.PlayerState,com.adobe.mediacore.MediaPlayerNotification%29" format="html" scope="external"> onStateChanged</a> (<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlayerState.html" format="html" scope="external"> MediaPlayer.PlayerState</a> 州/省， <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html" format="html" scope="external"> MediaPlayerNotification</a> notification) </td> 
   <td colname="2"> 媒体播放器的状态已更改。 您的应用程序应处理此回调中的错误。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onProfileChanged%28long,%20long%29" format="html" scope="external"> onProfileChanged</a> （长配置文件，长时间） </td> 
   <td colname="2"> 媒体播放器的当前配置文件已更改。 使用 <span class="codeph"> 个人资料</span> 属性以获取正在播放的新配置文件。 使用 <span class="codeph"> 时间</span> 属性，用于获取此事件发生时的时间。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>MediaplayerItem</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onUpdated%28%29" format="html" scope="external"> onUpdates</a> </td> 
   <td colname="2">在以下任一情况下，媒体播放器已成功更新媒体： 
    <ul> 
     <li>当实时资产发生清单刷新时。</li> 
     <li>当VOD或实时资产具有隐藏式字幕并且首次发现隐藏式字幕跟踪的活动时。 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>清单和时间线</b></td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimedMetadata%28com.adobe.mediacore.metadata.TimedMetadata%29" format="html" scope="external"> onTimedMetadata</a> (<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html" format="html" scope="external"> Timedatadata</a> timedMetadata) </td> 
   <td colname="2"> 在清单中发现新的定时元数据。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated%28%29" format="html" scope="external"> 时间线已更新</a> </td> 
   <td colname="2">媒体播放器已添加或删除广告，因此它拥有更新的时间轴。 <p>为实时资源刷新的清单并从时间轴中删除了旧的广告时间或发现了新的广告机会（提示点）。 媒体播放器会尝试解析任何新广告，并将其放在时间轴上。 </p><p> 使用此事件检查时间线是否有任何更新（播放期间VOD不会更改）。 然后，您可以使用检索时间轴 <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.html#getTimeline%28%29" format="html" scope="external"> MediaPlayer.getTimeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
