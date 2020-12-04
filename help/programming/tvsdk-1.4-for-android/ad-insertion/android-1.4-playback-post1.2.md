---
description: 媒体播放的行为受搜索、暂停、快进或后退（技巧播放模式）以及广告的包含的影响。
seo-description: 媒体播放的行为受搜索、暂停、快进或后退（技巧播放模式）以及广告的包含的影响。
seo-title: 使用广告的默认和自定义播放行为
title: 使用广告的默认和自定义播放行为
uuid: b977d7b5-bbae-4af4-92a7-0fdbffb08785
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---


# 广告{#default-and-customized-playback-behavior-with-ads}的默认和自定义播放行为

媒体播放的行为受搜索、暂停、快进或后退（技巧播放模式）以及广告的包含的影响。

要覆盖默认行为，请使用`AdBreakPolicySelector`。

>[!IMPORTANT]
>
>TVSDK不提供在广告期间禁用搜索的方法。 Adobe建议您将应用程序配置为在广告期间禁用搜索。

以下是实时／线性内容的播放行为：

* 在暂停后恢复播放会导致播放暂停时缓冲的内容。

   如果恢复位置仍在播放范围内，则播放应持续。 否则，TVSDK将跳转到新的实时点。 您还可以执行搜索操作并选择其他播放点。
* TVSDK解析应用程序进入实时回放位置后的提示之间的广告。

   解析第一个提示后，开始播放。 输入实时播放的默认值是客户端实时点，但您可以选择其他位置。 在应用程序在DVR窗口中执行搜索后，初始位置之前的所有提示都将被解析。

下表描述了TVSDK在播放过程中如何处理广告和广告中断：

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 视频活动 </th> 
   <th colname="col2" class="entry"> 默认TVSDK行为策略 </th> 
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
   <td colname="col3">使用<span class="codeph"> selectAdBreaksToPlay</span>选择要播放的跳过的分段，并使用<span class="codeph"> AdBreak.isWatched</span>确定已观看的分段。 <p>重要： 默认情况下，TVSDK在广告分段中输入第一个广告后立即将广告分段标记为已观看。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序会在一个或多个广告时段上向前或向后搜索，并进入已观看的广告时段。 </td> 
   <td colname="col2"> 跳过广告中断，在广告中断后立即找到相应位置。 </td> 
   <td colname="col3">使用<span class="codeph"> selectPolicyForSeekIntoAd</span>为广告中断（观察状态设置为true）和搜索结束的特定广告指定不同的广告策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序进入特技播放（DVR模式）。 播放速率可以为负（后退）或大于1（快进）。 </td> 
   <td colname="col2"> 在快进或后退期间跳过所有广告，在特技播放结束后播放最后跳过的休息，在该休息结束播放时跳到用户选择的特技播放位置。 </td> 
   <td colname="col3">使用<span class="codeph"> selectAdBreaksToPlay</span>选择特技播放结束后要播放的跳过的分段。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序会搜索使用自定义广告标记插入的广告。 </td> 
   <td colname="col2"> 跳转至用户选择的搜索位置。 </td> 
   <td colname="col3">有关详细信息，请参阅<a href="../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-seek-scrub-bar-display.md">使用当前播放位置</a>显示搜索拖拽栏。 </td> 
  </tr> 
 </tbody> 
</table>

