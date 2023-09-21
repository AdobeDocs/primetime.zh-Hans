---
description: 媒体播放行为受搜寻、暂停、快进或倒带（特技播放模式）以及包含广告的影响。
title: 默认和自定义的广告播放行为
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---

# 默认和自定义的广告播放行为 {#default-and-customized-playback-behavior-with-ads}

媒体播放行为受搜寻、暂停、快进或倒带（特技播放模式）以及包含广告的影响。

要覆盖默认行为，请使用 `AdBreakPolicySelector`.

>[!IMPORTANT]
>
>TVSDK不提供在广告期间禁用搜寻的方法。 Adobe建议您将应用程序配置为在广告期间禁用搜寻。

以下是实时/线性内容的播放行为：

* 暂停后恢复播放会导致播放暂停时缓冲的内容。

  如果恢复位置仍在播放范围内，则播放应是连续的。 否则，TVSDK将跳转到新的活动点。 也可以执行搜寻操作并选取其他回放点。
* TVSDK会在应用程序进入实时播放的位置之后解析提示之间的广告。

  在解析第一个提示后开始播放。 输入实时播放的默认值是客户端实时点，但您可以选择其他位置。 应用程序在DVR窗口中执行搜寻后，将解析初始位置之前的所有提示。

下表介绍了TVSDK在播放期间如何处理广告和广告时间：

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 视频活动 </th> 
   <th colname="col2" class="entry"> 默认TVSDK行为策略 </th> 
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
   <td colname="col3">选择要播放的跳过的断点 <span class="codeph"> selectAdBreaksToPlay</span> 并使用确定已查看的断点 <span class="codeph"> AdBreak.isWatched</span>. <p>重要信息：默认情况下，TVSDK在广告时间输入第一个广告后，会立即将广告时间标记为已观看。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序在一个或多个广告时间上向前或向后搜索，然后进入观看的广告时间。 </td> 
   <td colname="col2"> 跳过广告时间，并搜索广告时间后紧跟的位置。 </td> 
   <td colname="col3">为广告时间（观看状态设置为true）和搜寻结束的特定广告指定不同的广告策略 <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序进入特技播放（DVR模式）。 播放率可以为负（倒带）或大于1（快进）。 </td> 
   <td colname="col2"> 在快进或倒带期间跳过所有广告，播放特技播放结束后跳过的最后一个中断，并在该中断完成播放时跳过到用户选择的特技播放位置。 </td> 
   <td colname="col3">使用以下方式选择要在特技播放结束后播放的跳过休息时间 <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的应用程序向前搜寻使用自定义广告标记插入的广告。 </td> 
   <td colname="col2"> 跳至用户选择的搜寻位置。 </td> 
   <td colname="col3">有关更多信息，请参阅 <a href="../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-seek-scrub-bar-display.md">显示具有当前播放位置的搜寻拖拽栏</a>. </td> 
  </tr> 
 </tbody> 
</table>
