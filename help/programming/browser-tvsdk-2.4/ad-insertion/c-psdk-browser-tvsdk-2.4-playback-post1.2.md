---
description: 媒体播放行为受搜寻、暂停、快进或倒带（特技播放模式）以及包含广告的影响。
title: 默认和自定义的广告播放行为
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# 默认和自定义的广告播放行为{#default-and-customized-playback-behavior-with-ads}

媒体播放行为受搜寻、暂停、快进或倒带（特技播放模式）以及包含广告的影响。

要覆盖默认行为，请使用 `AdBreakPolicySelector`.

>[!IMPORTANT]
>
>浏览器TVSDK不提供在广告期间禁用搜寻的方法。 Adobe建议您将应用程序配置为在广告期间禁用搜寻。

下表描述了浏览器TVSDK在播放期间如何处理广告和广告时间：

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 视频活动 </th> 
   <th colname="col2" class="entry"> 默认浏览器TVSDK行为策略 </th> 
   <th colname="col3" class="entry">可通过以下方式自定义 <span class="codeph"> AdBreakPolicySelect </span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 在正常播放期间，遇到广告时间。 </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> 对于实时/线性，即使已观看广告时间，也会播放广告时间。 </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">对于VOD，播放广告时间并将广告时间标记为已观看。 </li> 
    </ul> </td> 
   <td colname="col3">使用以下方式为广告时间指定其他策略 <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序在广告时间中向前寻求进入主内容。 </td> 
   <td colname="col2"> 播放上一个跳过且未被观看的广告时间，并在广告时间播放完成后在所需的搜寻位置恢复播放。 </td> 
   <td colname="col3">使用以下方式选择要播放的跳过的休息时间 <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序向后搜索广告时间，以将其转换为主内容。 </td> 
   <td colname="col2"> 跳到所需的搜寻位置而不播放广告时间。 </td> 
   <td colname="col3">使用以下方式选择要播放的跳过的休息时间 <span class="codeph"> selectAdBreaksToPlay</span>.                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序将尝试进入广告时间。 </td> 
   <td colname="col2"> 从搜寻结束的广告开始播放。 </td> 
   <td colname="col3">为广告时间以及搜寻结束的特定广告指定不同的广告策略 <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序向后搜索进入广告时间。 </td> 
   <td colname="col2"> 从搜寻结束的广告开始播放。 </td> 
   <td colname="col3">为广告时间以及搜寻结束的特定广告指定不同的广告策略 <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序在观看广告时间后向前或向后搜索主内容。 </td> 
   <td colname="col2"> 如果跳过的最后一个广告时间已被观看，则会跳至用户选择的搜寻位置。 </td> 
   <td colname="col3">选择要播放的跳过的断点 <span class="codeph"> selectAdBreaksToPlay</span> 并使用确定已查看的断点 <span class="codeph"> isWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序在一个或多个广告时间上向前或向后搜索，然后进入观看的广告时间。 </td> 
   <td colname="col2"> 跳过广告时间，并搜索广告时间后紧跟的位置。 </td> 
   <td colname="col3">为广告时间（观看状态设置为true）和搜寻结束的特定广告指定不同的广告策略 <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序向前搜寻使用自定义广告标记插入的广告。 </td> 
   <td colname="col2"> 跳至用户选择的搜寻位置。 </td> 
   <td colname="col3">有关更多信息，请参阅 <a href="../../browser-tvsdk-2.4/content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> 使用搜寻栏时处理搜寻</a> </td> 
  </tr> 
 </tbody> 
</table>

## 设置自定义广告行为 {#section_custom_ad_behaviors}

您可以在广告内容工厂中设置您的首选行为 `retrieveAdPolicySelectorCallbackFunc` 方法。 您可以使用 `selectPolicyForAdBreak`， `selectWatchedPolicyForAdBreak`， `selectPolicyForSeekIntoAd`、和 `selectAdBreaksToPlay` 内容工厂中选择策略的方法。
