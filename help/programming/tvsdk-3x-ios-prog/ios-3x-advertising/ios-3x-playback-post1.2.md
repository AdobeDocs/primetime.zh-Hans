---
description: 媒体播放的行为受搜索、暂停和广告的包含的影响。
seo-description: 媒体播放的行为受搜索、暂停和广告的包含的影响。
seo-title: 使用广告的默认和自定义播放行为
title: 使用广告的默认和自定义播放行为
uuid: 570f6d77-cbb9-4aa7-a935-058003f4ce87
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# 广告{#default-and-customized-playback-behavior-with-ads}的默认和自定义播放行为

媒体播放的行为受搜索、暂停和广告的包含的影响。

要覆盖默认行为，请使用`PTAdPolicySelector`。

>[!IMPORTANT]
>
>对于VOD和实时／线性流，无法修改时间轴调整。 这意味着播放广告后，无法从时间轴中删除该广告。 如果用户进行搜索，则同一广告将再次播放，即使正常的策略是删除它。

>[!IMPORTANT]
>
>TVSDK不提供在广告期间禁用搜索的方法。 Adobe建议您将应用程序配置为在广告期间禁用搜索。

下表描述了TVSDK在播放过程中如何处理广告和广告中断：

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>视频活动</b></th> 
   <th colname="col2" class="entry"><b>默认TVSDK行为策略</b></th> 
   <th colname="col3" class="entry"><b>可通过PTAdPolicySelector进行自定义</b></th>
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 在正常播放期间，会遇到广告中断。 </td> 
   <td colname="col2"></td> 
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
   <td colname="col3">使用<span class="codeph"> selectAdBreaksToPlay</span>选择要播放的跳过的分段，并使用<span class="codeph"> PTAdBreak.isWatched</span>确定已观看的分段。 <p> <p>重要： 默认情况下，TVSDK在广告分段中输入第一个广告后立即将广告分段标记为已观看。 </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序会在一个或多个广告时段上向前或向后搜索，并进入已观看的广告时段。 </td> 
   <td colname="col2"> 跳过广告中断，在广告中断后立即找到相应位置。 </td> 
   <td colname="col3">使用<span class="codeph"> selectPolicyForSeekIntoAd</span>为广告中断（观察状态设置为true）和搜索结束的特定广告指定不同的广告策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序会搜索使用自定义广告标记插入的广告。 </td> 
   <td colname="col2"> 跳转至用户选择的搜索位置。 </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>