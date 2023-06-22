---
description: HLS和DASH流为同一短突发视频提供不同的比特率编码（配置文件）。 TVSDK可以根据可用带宽选择每个突发的质量级别。
title: 用于视频质量的自适应比特率(ABR)
exl-id: d5bcce93-9bd1-45cf-a4c4-bec97476f560
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# 概述 {#adaptive-bit-rates-abr-for-video-quality-overview}

HLS和DASH流为同一短突发视频提供不同的比特率编码（配置文件）。 TVSDK可以根据可用带宽选择每个突发的质量级别。

TVSDK会持续监控比特率，以确保内容以当前网络连接的最佳比特率播放。

您可以为多比特率(MBR)流设置自适应比特率(ABR)切换策略以及初始、最小和最大比特率。 TVSDK会自动切换到在指定配置中提供最佳播放体验的比特率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始比特率 </td> 
   <td colname="col2"> <p>第一段所需的播放比特率（以位/秒为单位）。 当播放开始时，第一个区段使用最接近的配置文件，该配置文件等于或大于初始比特率。 </p> <p> 如果定义了最小比特率，并且初始比特率低于最小比特率，则TVSDK选择最低比特率高于最小比特率的配置文件。 如果初始速率高于最大速率，TVSDK会选择低于最大速率的最高速率。 </p> <p>如果初始比特率为零或未定义，则初始比特率由ABR策略确定。 </p> <p><span class="codeph"> getABRIinitialBitRate</span> 返回表示每秒字节配置文件的整数值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小比特率 </td> 
   <td colname="col2"> <p>ABR可切换的最低允许比特率。 ABR切换将忽略比特率低于此比特率的配置文件。 </p> <p><span class="codeph"> getabriminbitrate</span> 返回一个整数值，该值表示每秒位数的配置文件。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2"> <p>ABR可以切换到的允许的最高比特率。 ABR切换忽略比特率高于此比特率的配置文件。 </p> <p><span class="codeph"> getABRMaxBitRate</span> 返回一个整数值，该值表示每秒位数的配置文件。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR切换策略 </td> 
   <td colname="col2"> 如果可能，播放将逐渐切换到最高比特率配置文件。 您可以设置ABR切换策略，以确定TVSDK在配置文件之间切换的速度。 默认为 <span class="codeph"> ABR_MODERATE</span>. <p>当TVSDK决定切换到更高的比特率时，播放器根据当前的ABR策略选择理想的比特率配置文件来切换到： 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_保守</span>：当带宽比当前比特率高50%时，切换到具有下一较高比特率的配置文件。 </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MODERATE</span>：当带宽比当前比特率高20%时，切换到下一个更高的比特率配置文件。 </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_AGGRESSIVE</span>：当带宽高于当前比特率时，立即切换到最高比特率配置文件。 </li> 
     </ul> </p> <p>如果初始比特率为零或未指定，但指定了策略，则播放开始时将采用最低比特率配置文件（对于保守策略）、最接近可用配置文件的中位比特率的配置文件（对于中等策略）以及最高比特率配置文件（对于激进策略）。 </p> <p>如果指定了最小和最大比特率，则该策略将在约束下工作。 </p> <p><span class="codeph"> getABRPolicy</span> 返回当前设置来自 <span class="codeph"> ABRControlParameters</span> 枚举： 
     <ul id="ul_bd4_5kb_cz"> 
      <li id="li_E7C118AF48994454B7B3C016913DE545"><span class="codeph"> ABR_保守</span> </li> 
      <li id="li_0A90BB42786449629CE7DD3364B385EE"><span class="codeph"> ABR_MODERATE</span> </li> 
      <li id="li_AFEB9B2862F24A369CA90596184A2883"><span class="codeph"> ABR_AGGRESSIVE</span> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

请牢记以下信息：

* TVSDK故障转移机制可能会覆盖您的设置，因为TVSDK更喜欢连续播放体验，而不是严格遵守控制参数。
* 当比特率改变时，TVSDK调度 `onProfileChanged` 中的事件 `PlaybackEventListener`.

* 您可以随时更改ABR设置，播放器将切换为使用与最新设置最匹配的配置文件。

例如，如果流具有以下配置文件：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果指定300000到2000000的范围，TVSDK仅考虑用户档案1、2和3。 这允许应用程序适应各种网络条件，例如从Wi-Fi切换到3G或各种设备，如手机、平板电脑或台式计算机。

要设置ABR控制参数，请在 `ABRControlParameter` 类。
