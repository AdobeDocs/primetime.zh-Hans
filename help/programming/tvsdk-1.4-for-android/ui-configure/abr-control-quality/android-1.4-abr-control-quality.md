---
description: HLS和DASH流为同一短视频突发提供不同的比特率编码(用户档案)。 TVSDK可以根据可用带宽为每个突发选择质量级别。
seo-description: HLS和DASH流为同一短视频突发提供不同的比特率编码(用户档案)。 TVSDK可以根据可用带宽为每个突发选择质量级别。
seo-title: 视频质量的自适应比特率(ABR)
title: 视频质量的自适应比特率(ABR)
uuid: 1de26f34-4eac-4c9c-8f59-8c34d69a2d01
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---


# 概述{#adaptive-bit-rates-abr-for-video-quality-overview}

HLS和DASH流为同一短视频突发提供不同的比特率编码(用户档案)。 TVSDK可以根据可用带宽为每个突发选择质量级别。

TVSDK会持续监视比特率，以确保以当前网络连接的最佳比特率播放内容。

可以为多比特率(MBR)流设置自适应比特率(ABR)切换策略以及初始、最小和最大比特率。 TVSDK自动切换到在指定配置中提供最佳播放体验的比特率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始比特率 </td> 
   <td colname="col2"> <p>第一段的所需回放位速率（以位／秒为单位）。 当播放开始时，对于第一段使用等于或大于初始比特率的最接近用户档案。 </p> <p> 如果定义了最小比特率，并且初始比特率低于最小速率，则TVSDK选择具有高于最小比特率的最低比特率的用户档案。 如果初始速率高于最大速率，则TVSDK将选择低于最大速率的最高速率。 </p> <p>如果初始比特率为零或未定义，则初始比特率由ABR策略确定。 </p> <p><span class="codeph"> </span> getABRInitialBitRate返回一个整数值，它表示每秒字节用户档案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小比特率 </td> 
   <td colname="col2"> <p>ABR可以切换到的允许的最低比特率。 ABR切换忽略比特率低于此比特率的用户档案。 </p> <p><span class="codeph"> </span> getABRMinBitRate返回一个整数值，它表示每秒的位用户档案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2"> <p>ABR可以切换到的允许的最高比特率。 ABR切换忽略比特率高于此比特率的用户档案。 </p> <p><span class="codeph"> </span> getABRMaxBitRate返回一个整数值，它表示每秒的位用户档案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR切换策略 </td> 
   <td colname="col2"> 回放功能会尽可能逐渐切换到最高比特率的用户档案。 您可以设置ABR切换策略，该策略确定TVSDK在用户档案之间切换的速度。 默认值为<span class="codeph"> ABR_MEDEATE</span>。 <p>当TVSDK决定切换到更高的比特率时，播放器会根据当前的ABR策略选择理想的比特率用户档案来切换： 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_CONSERTIC</span>:当带宽比当前比特率高50%时，切换到用户档案，其下一个比特率更高。 </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MEDEATE</span>:当带宽比当前比特率高20%时，切换到下一个较高的比特率用户档案。 </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_ACCORSIVE</span>:当带宽高于当前比特率时，立即切换到最高比特率用户档案。 </li> 
     </ul> </p> <p>如果初始比特率为零或未指定，但指定了策略，则播放开始的比特率用户档案最低（保守），最接近中等可用用户档案的中位比特率的用户档案，以及攻击性的最高比特率用户档案。 </p> <p>如果指定了这些速率，则策略在最小比特率和最大比特率的约束下有效。 </p> <p><span class="codeph"> </span> getABRPolicyle从ABRControlParametersenum返回当 <span class="codeph"> </span> 前设置： 
     <ul id="ul_bd4_5kb_cz"> 
      <li id="li_E7C118AF48994454B7B3C016913DE545"><span class="codeph"> ABR_CONSURACY</span> </li> 
      <li id="li_0A90BB42786449629CE7DD3364B385EE"><span class="codeph"> ABR_MEDEATE</span> </li> 
      <li id="li_AFEB9B2862F24A369CA90596184A2883"><span class="codeph"> ABR_ACCORSIVE</span> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

请记住以下信息：

* TVSDK故障切换机制可能会覆盖您的设置，因为TVSDK更青睐连续播放体验，而不是严格遵循您的控制参数。
* 当位速率发生变化时，TVSDK在`PlaybackEventListener`中调度`onProfileChanged`事件。

* 您可以随时更改ABR设置，播放器会切换为使用与最近设置最接近的用户档案。

例如，如果流具有以下用户档案:

* 1:300000
* 2:700000
* 3:1500000
* 4:2400000
* 5:4000000

如果指定的范围是3000000到20000000，则TVSDK仅考虑用户档案1、2和3。 这使应用程序能够适应各种网络条件，如从wi-fi切换到3G或切换到手机、平板电脑或台式计算机等各种设备。

要设置ABR控制参数，请在`ABRControlParameter`类上设置参数。
