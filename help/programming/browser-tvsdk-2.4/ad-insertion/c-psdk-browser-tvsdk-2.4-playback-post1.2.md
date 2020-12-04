---
description: 媒体播放的行为受搜索、暂停、快进或后退（技巧播放模式）以及广告的包含的影响。
seo-description: 媒体播放的行为受搜索、暂停、快进或后退（技巧播放模式）以及广告的包含的影响。
seo-title: 使用广告的默认和自定义播放行为
title: 使用广告的默认和自定义播放行为
uuid: 58f11167-a764-4647-8490-05ca66eb6c47
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# 广告的默认和自定义播放行为{#default-and-customized-playback-behavior-with-ads}

媒体播放的行为受搜索、暂停、快进或后退（技巧播放模式）以及广告的包含的影响。

要覆盖默认行为，请使用`AdBreakPolicySelector`。

>[!IMPORTANT]
>
>浏览器TVSDK不提供在广告期间禁用搜索的方法。 Adobe建议您将应用程序配置为在广告期间禁用搜索。

下表描述了Browser TVSDK在播放过程中如何处理广告和广告中断：

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 视频活动 </th> 
   <th colname="col2" class="entry"> 默认浏览器TVSDK行为策略 </th> 
   <th colname="col3" class="entry">可通过<span class="codeph"> AdBreakPolicySelector </span>进行自定义 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 在正常播放期间，会遇到广告中断。 </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> 对于实时／线性，播放广告中断，即使广告中断已被观看。 </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">对于VOD，播放广告分段并将广告分段标记为已观看。 </li> 
    </ul> </td> 
   <td colname="col3">使用<span class="codeph"> selectPolicyForAdBreak</span>为广告中断指定不同的策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序会逐个广告转向主内容。 </td> 
   <td colname="col2"> 在中断播放完成时，播放上次跳过的未观看广告中断，并在所需的搜索位置恢复播放。 </td> 
   <td colname="col3">使用<span class="codeph"> selectAdBreaksToPlay</span>选择要播放的跳过的中断。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序会在广告中向后搜索主内容。 </td> 
   <td colname="col2"> 跳至所需的搜索位置，而不播放广告分段。 </td> 
   <td colname="col3">使用<span class="codeph"> selectAdBreaksToPlay</span>选择要播放的跳过的中断。                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序将进入广告中断。 </td> 
   <td colname="col2"> 从搜索结束的广告开始播放。 </td> 
   <td colname="col3">使用<span class="codeph"> selectPolicyForSeekIntoAd</span>为广告中断和搜索结束的特定广告指定不同的广告策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序会向后搜索到广告中断。 </td> 
   <td colname="col2"> 从搜索结束的广告开始播放。 </td> 
   <td colname="col3">使用<span class="codeph"> selectPolicyForSeekIntoAd</span>为广告中断和搜索结束的特定广告指定不同的广告策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序在观看的广告中向前或向后搜索主内容。 </td> 
   <td colname="col2"> 如果已观看上次跳过的广告，则跳转到用户选择的搜索位置。 </td> 
   <td colname="col3">使用<span class="codeph"> selectAdBreaksToPlay</span>选择要播放的跳过的分段，并使用<span class="codeph"> isWatched</span>确定已观看的分段。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序会在一个或多个广告时段上向前或向后搜索，并进入已观看的广告时段。 </td> 
   <td colname="col2"> 跳过广告中断，在广告中断后立即找到相应位置。 </td> 
   <td colname="col3">使用<span class="codeph"> selectPolicyForSeekIntoAd</span>为广告中断（观察状态设置为true）和搜索结束的特定广告指定不同的广告策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序会搜索使用自定义广告标记插入的广告。 </td> 
   <td colname="col2"> 跳转至用户选择的搜索位置。 </td> 
   <td colname="col3">有关详细信息，请参阅<a href="../../browser-tvsdk-2.4/content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-seek-scrub-bar-display.md" format="dita" scope="local">使用搜索栏时处理搜索</a> </td> 
  </tr> 
 </tbody> 
</table>

## 设置自定义广告行为{#section_custom_ad_behaviors}

可以在`retrieveAdPolicySelectorCallbackFunc`方法的广告内容工厂中设置首选行为。 您可以在内容工厂中使用`selectPolicyForAdBreak`、`selectWatchedPolicyForAdBreak`、`selectPolicyForSeekIntoAd`和`selectAdBreaksToPlay`方法来选择策略。
