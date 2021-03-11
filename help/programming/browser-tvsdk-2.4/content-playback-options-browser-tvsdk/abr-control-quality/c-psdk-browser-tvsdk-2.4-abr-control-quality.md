---
description: HLS和DASH流为同一短视频突发提供不同的比特率编码(用户档案)。 浏览器TVSDK可以根据可用带宽为每个突发选择质量级别。
title: 用于视频质量的自适应比特率(ABR)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---


# 概述{#adaptive-bit-rates-abr-for-video-quality-overview}

HLS和DASH流为同一短视频突发提供不同的比特率编码(用户档案)。 浏览器TVSDK可以根据可用带宽为每个突发选择质量级别。

浏览器TVSDK会持续监视比特率，以确保内容以当前网络连接的最佳比特率播放。

可以设置自适应比特率(ABR)切换策略以及多比特率(MBR)流的初始、最小和最大比特率。 浏览器TVSDK自动切换到在指定配置中提供最佳播放体验的比特率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始比特率 </td> 
   <td colname="col2">第一段的所需回放比特率（以位/秒为单位）。 当播放开始时，第一段使用最接近的用户档案，即等于或大于初始比特率。 <p> 如果定义了最小比特率，并且初始比特率低于最小速率，则Browser TVSDK选择比特率最低的用户档案高于最小比特率。 如果初始速率高于最大速率，Browser TVSDK将选择低于最大速率的最高速率。 </p> <p>如果初始比特率为零或未定义，则初始比特率由ABR策略确定。 </p> <p><span class="codeph"> </span> initialBitRate返回一个整数值，它表示每秒字节的用户档案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小比特率 </td> 
   <td colname="col2">ABR可切换到的允许的最低位速率。 ABR切换忽略比特率低于此比特率的用户档案。 <p><span class="codeph"> </span> minBitRate返回一个整数值，它表示每秒的位用户档案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2">ABR可切换到的最高允许位速率。 ABR切换忽略比特率高于此比特率的用户档案。 <p><span class="codeph"> </span> maxBitRate返回一个整数值，它表示每秒的位用户档案。 </p> </td> 
  </tr> 
 </tbody> 
</table>

请记住以下信息：

* 当位速率更改时，Browser TVSDK将调度类型为`AdobePSDK.PSDKEventType.PROFILE_CHANGED`的`AdobePSDK.ProfileEvent`。

* 您可以随时更改ABR设置，播放器会切换以使用与最新设置最接近的用户档案。

例如，如果流具有以下用户档案:

* 1:300000
* 2:700000
* 3:1500000
* 4:2400000
* 5:4000000

如果您指定的范围为300000到2000000，则浏览器TVSDK仅考虑用户档案1、2和3。 这使应用程序能够适应各种网络条件，如从wi-fi切换到3G，或切换到手机、平板电脑或台式计算机等各种设备。

要设置ABR控制参数：

* 在`ABRControlParameters`类上设置参数。

