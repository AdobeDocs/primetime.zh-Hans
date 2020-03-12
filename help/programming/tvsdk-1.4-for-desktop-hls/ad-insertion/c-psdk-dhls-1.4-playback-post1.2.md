---
description: 媒体播放的行为受搜索、暂停、快进或后退（特技播放模式）以及包含广告的影响。
seo-description: 媒体播放的行为受搜索、暂停、快进或后退（特技播放模式）以及包含广告的影响。
seo-title: 使用广告默认和自定义的播放行为
title: 使用广告默认和自定义的播放行为
uuid: 45e6b0cd-fb0b-4896-b53a-d3bd78a3c1f3
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184

---


# 使用广告默认和自定义的播放行为{#default-and-customized-playback-behavior-with-ads}

媒体播放的行为受搜索、暂停、快进或后退（特技播放模式）以及包含广告的影响。

要覆盖默认行为，请使用 `AdPolicySelector`。

>[!IMPORTANT]
>
>TVSDK不提供在广告期间禁用搜索的方法。 Adobe建议您将应用程序配置为在广告期间禁用搜索。

下表介绍了TVSDK在播放过程中如何处理广告和广告中断：

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 视频活动 </th> 
   <th colname="col2" class="entry"> 默认TVSDK行为策略 </th> 
   <th colname="col3" class="entry">可通过AdPolicySelector进行自定 <span class="codeph"> 义</span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 在正常播放期间，会遇到广告中断。 </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> 对于实时／线性，播放广告分段，即使广告分段已被观看也是如此。 </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">对于VOD，播放广告分段并将广告分段标记为已观看。 </li> 
    </ul> </td> 
   <td colname="col3">使用selectPolicyForAdBreak为广告中断指定其 <span class="codeph"> 他策略</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序会逐个向前搜索到主要内容。 </td> 
   <td colname="col2"> 播放上次未观看的广告中断，该广告中断被跳过，并在中断播放完成时在所需的搜索位置继续播放。 </td> 
   <td colname="col3">使用selectAdBreaksToPlay选择要播放的跳过的 <span class="codeph"> 分段</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序会逐个向后搜索主内容。 </td> 
   <td colname="col2"> 跳转到所需的搜索位置，而不播放广告中断。 </td> 
   <td colname="col3">使用selectAdBreaksToPlay选择要播放的跳过的 <span class="codeph"> 分段</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序将进入广告分时段。 </td> 
   <td colname="col2"> 从搜索结束的广告开始播放。 </td> 
   <td colname="col3">使用selectPolicyForSeekIntoAd为广告中断和搜索结束的特定广告指定不同的广 <span class="codeph"> 告策略</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序会向后搜索到广告中断。 </td> 
   <td colname="col2"> 从搜索结束的广告开始播放。 </td> 
   <td colname="col3">使用selectPolicyForSeekIntoAd为广告中断和搜索结束的特定广告指定不同的广 <span class="codeph"> 告策略</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序在观看的广告中向前或向后搜索到主内容。 </td> 
   <td colname="col2"> 如果已观看最后一个跳过的广告中断，则跳转到用户选择的搜索位置。 </td> 
   <td colname="col3">使用selectAdBreaksToPlay选择要播放的跳过的分 <span class="codeph"> 段</span> ，并使用TimeLineItem.watched确定已观看的分 <span class="codeph"> 段</span> 。 <p>重要说明： 默认情况下，TVSDK在广告分段中输入第一个广告后立即将广告分段标记为已观看。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序在一个或多个广告分段中向前或向后搜索，并进入一个观看的广告分段。 </td> 
   <td colname="col2"> 跳过广告中断，并在广告中断后立即寻找位置。 </td> 
   <td colname="col3">为广告中断（观察状态设置为true）以及通过使用selectPolicyForSeekIntoAd结束搜索的特定广告指定其他广 <span class="codeph"> 告策略</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 应用程序进入特技播放（DVR模式）。 播放率可为负（后退）或大于1（快进）。 </td> 
   <td colname="col2"> 在快进或后退期间跳过所有广告，在特技播放结束后播放最后跳过的中断，并在该中断完成播放时跳到用户选择的特技播放位置。 </td> 
   <td colname="col3">使用selectAdBreaksToPlay选择特技播放结束后要播放的跳过的分 <span class="codeph"> 段之一</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序会搜索使用自定义广告标记插入的广告。 </td> 
   <td colname="col2"> 跳转至用户选择的搜索位置。 </td> 
   <td colname="col3">有关详细信息，请 <a href="../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> 参阅显示具有当前播放位置的搜索拖拽栏……</a> </td> 
  </tr> 
 </tbody> 
</table>

