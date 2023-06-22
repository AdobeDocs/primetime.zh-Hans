---
description: 媒体播放行为受搜寻、暂停和包含广告的影响。
title: 默认和自定义的广告播放行为
exl-id: bd92b58a-fc71-41de-a80e-19002d66246f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# 默认和自定义的广告播放行为{#default-and-customized-playback-behavior-with-ads}

媒体播放行为受搜寻、暂停和包含广告的影响。

要覆盖默认行为，请使用 `PTAdPolicySelector`.

>[!IMPORTANT]
>
>对于VOD和实时/线性流，无法修订时间线调整。 这意味着播发在播放后无法从时间轴中删除。 如果用户回头搜索，则即使正常策略是删除同一广告，也会再次播放该广告。

>[!IMPORTANT]
>
>TVSDK不提供在广告期间禁用搜寻的方法。 Adobe建议您将应用程序配置为在广告期间禁用搜寻。

下表介绍了TVSDK在播放期间如何处理广告和广告时间：

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 视频活动 </th> 
   <th colname="col2" class="entry"> 默认TVSDK行为策略 </th> 
   <th colname="col3" class="entry">可通过以下方式自定义 <span class="codeph"> ptadPolicySelector</span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 在正常播放期间，遇到广告时间。 </td> 
   <td colname="col2"></td> 
   <td colname="col3">使用以下方式为广告时间指定其他策略 <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序在广告时间上向前搜索以进入主内容。 </td> 
   <td colname="col2"> 播放上一个跳过且未被观看的广告时间，并在广告时间播放完成后在所需的搜寻位置恢复播放。 </td> 
   <td colname="col3">使用以下方式选择要播放的跳过的断点 <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序向后搜索广告插播，以进入主内容。 </td> 
   <td colname="col2"> 跳至所需的搜寻位置而不播放广告时间。 </td> 
   <td colname="col3">使用以下方式选择要播放的跳过的断点 <span class="codeph"> selectAdBreaksToPlay</span>.                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序将尝试进入广告时间。 </td> 
   <td colname="col2"> 从搜寻结束的广告开始播放。 </td> 
   <td colname="col3">为广告时间以及搜寻结束的特定广告指定不同的广告策略 <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序向后搜索进入广告时间。 </td> 
   <td colname="col2"> 从搜寻结束的广告开始播放。 </td> 
   <td colname="col3">为广告时间指定其他广告策略，并为使用结束搜寻的特定广告指定其他广告策略 <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序在观看广告时间后向前或向后搜索主内容。 </td> 
   <td colname="col2"> 如果跳过的最后一个广告时间已被观看，则会跳至用户选择的搜寻位置。 </td> 
   <td colname="col3">选择要播放的跳过的断点 <span class="codeph"> selectAdBreaksToPlay</span> 并确定已使用观察了哪些中断 <span class="codeph"> ptadBreak.isWatched</span>. <p> <p>重要信息：默认情况下，TVSDK在广告时间中输入第一个广告后，会立即将广告时间标记为已观看。 </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序在一个或多个广告时间上向前或向后搜索，然后进入观看的广告时间。 </td> 
   <td colname="col2"> 跳过广告时间，并搜索紧跟广告时间之后的位置。 </td> 
   <td colname="col3">为广告时间（观看状态设置为true）和搜寻结束的特定广告指定不同的广告策略 <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序会向前搜索使用自定义广告标记插入的广告。 </td> 
   <td colname="col2"> 跳至用户选择的搜寻位置。 </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>
