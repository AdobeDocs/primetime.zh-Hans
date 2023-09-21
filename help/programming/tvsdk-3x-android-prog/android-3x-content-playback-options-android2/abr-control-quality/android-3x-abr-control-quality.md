---
description: HLS和DASH流为相同的短突发视频提供不同的比特率编码（配置文件）。 TVSDK可以根据当前缓冲级别和可用带宽为每个突发选择质量级别。
title: 用于视频质量的自适应比特率(ABR)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# 概述 {#adaptive-bit-rates-abr-for-video-quality-overview}

HLS和DASH流为相同的短突发视频提供不同的比特率编码（配置文件）。 TVSDK可以根据当前缓冲级别和可用带宽为每个突发选择质量级别。

TVSDK会持续监控比特率，以确保在当前网络连接中以最佳比特率播放内容。 您可以设置自适应比特率(ABR)切换策略以及多比特率(MBR)流的初始、最小和最大比特率。 TVSDK会自动切换到在指定配置中提供最佳播放体验的比特率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始比特率 </td> 
   <td colname="col2"> <p>第一段所需的播放比特率（位/秒）。 </p> <p>开始播放时，第一个区段使用最接近的配置文件，该配置文件等于或大于初始比特率。 如果定义了最小比特率，并且初始比特率低于最小比特率，则TVSDK选择最低比特率高于最小比特率的配置文件。 如果初始速率高于最大速率，TVSDK将选择低于最大速率的最高速率。 如果初始比特率为零或未定义，则初始比特率由ABR策略确定。 </p> <p><span class="codeph"> getABRIinitialBitRate</span> 返回表示每秒字节配置文件的整数值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小比特率 </td> 
   <td colname="col2"> <p>ABR可切换的最低允许比特率。 </p> <p>ABR切换将忽略比特率低于此比特率的配置文件。 <span class="codeph"> getABRMinBitrate</span> 返回表示每秒位配置文件的整数值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2"> <p>ABR可切换的最高允许比特率。 </p> <p>ABR切换将忽略比特率高于此比特率的配置文件。 <span class="codeph"> getABRMaxBitRate</span> 返回表示每秒位配置文件的整数值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR切换策略 </td> 
   <td colname="col2"> <p>如果可能，播放将逐渐切换到最高比特率配置文件。 您可以设置ABR切换策略，该策略可决定TVSDK在配置文件之间切换的速度。 默认为 <span class="codeph"> ABR_MODERATE</span>. </p> <p>当TVSDK决定切换到更高的比特率时，播放器根据当前ABR策略选择理想的比特率配置文件以切换到： 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_保守</span>：当带宽比当前比特率高50%时，切换到具有下一更高比特率的配置文件。 </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MODERATE</span>：当带宽比当前比特率高20%时，切换到下一个更高的比特率配置文件。 </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_AGGRESSIVE</span>：当带宽高于当前比特率时，立即切换到最高比特率配置文件。 </li> 
     </ul> </p> <p>如果初始比特率为零或未指定但指定了策略，则对于保守策略，从最低比特率配置文件开始；对于中等策略，从最接近可用配置文件中间比特率的配置文件开始；对于积极策略，从最高比特率配置文件开始。 </p> <p>如果指定了最小和最大比特率，则该策略将在约束下工作。 </p> <p> <span class="codeph"> getABRPolicy</span> 返回当前设置，从 <span class="codeph"> ABRControlParameters</span> 枚举： <span class="codeph"> ABR_保守</span>， <span class="codeph"> ABR_MODERATE</span>，或 <span class="codeph"> ABR_AGGRESSIVE</span>. </p> <p>有关详细信息，请参阅ABR控制参数API文档。 </p> </td> 
  </tr> 
 </tbody> 
</table>

请牢记以下信息：

* TVSDK故障转移机制可能会覆盖您的设置，因为TVSDK更倾向于持续播放体验，而不是严格遵守控制参数。
* 当比特率发生更改时，TVSDK将调度 `onProfileChanged` 中的事件 `PlaybackEventListener`.

* 您可以随时更改ABR设置，播放器将切换为使用与最新设置最匹配的配置文件。

例如，如果流具有以下配置文件：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果指定300000到2000000的范围，TVSDK将仅考虑用户档案1、2和3。 这允许应用程序适应各种网络条件，例如从wi-fi切换到3G或各种设备，如手机、平板电脑或台式计算机。

要设置ABR控制参数，请在 `ABRControlParameter` 类。
