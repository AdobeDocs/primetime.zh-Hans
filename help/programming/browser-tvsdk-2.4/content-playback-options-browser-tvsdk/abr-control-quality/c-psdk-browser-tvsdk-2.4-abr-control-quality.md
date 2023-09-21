---
description: HLS和DASH流为相同的短突发视频提供不同的比特率编码（配置文件）。 浏览器TVSDK可以根据可用带宽选择每个突发的质量级别。
title: 用于视频质量的自适应比特率(ABR)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---

# 概述 {#adaptive-bit-rates-abr-for-video-quality-overview}

HLS和DASH流为相同的短突发视频提供不同的比特率编码（配置文件）。 浏览器TVSDK可以根据可用带宽选择每个突发的质量级别。

浏览器TVSDK会持续监控比特率，以确保在当前网络连接中以最佳比特率播放内容。

您可以设置自适应比特率(ABR)切换策略以及多比特率(MBR)流的初始、最小和最大比特率。 浏览器TVSDK会自动切换到在指定配置中提供最佳播放体验的比特率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始比特率 </td> 
   <td colname="col2">第一段所需的播放比特率（位/秒）。 开始播放时，第一个区段使用最接近的配置文件，该配置文件等于或大于初始比特率。 <p> 如果定义了最小比特率，并且初始比特率低于最小比特率，则浏览器TVSDK选择最低比特率高于最小比特率的配置文件。 如果初始速率高于最大速率，浏览器TVSDK会选择低于最大速率的最高速率。 </p> <p>如果初始比特率为零或未定义，则初始比特率由ABR策略确定。 </p> <p><span class="codeph"> 初始比特率</span> 返回表示每秒字节配置文件的整数值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小比特率 </td> 
   <td colname="col2">ABR可切换的最低允许比特率。 ABR切换将忽略比特率低于此比特率的配置文件。 <p><span class="codeph"> minBitRate</span> 返回表示每秒位配置文件的整数值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2">ABR可切换的最高允许比特率。 ABR切换将忽略比特率高于此比特率的配置文件。 <p><span class="codeph"> maxBitRate</span> 返回表示每秒位配置文件的整数值。 </p> </td> 
  </tr> 
 </tbody> 
</table>

请牢记以下信息：

* 当比特率更改时，浏览器TVSDK调度 `AdobePSDK.ProfileEvent` 类型为 `AdobePSDK.PSDKEventType.PROFILE_CHANGED`.

* 您可以随时更改ABR设置，播放器将切换为使用与最新设置最匹配的配置文件。

例如，如果流具有以下配置文件：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果指定300000到2000000的范围，则浏览器TVSDK仅考虑用户档案1、2和3。 这允许应用程序适应各种网络条件，例如从wi-fi切换到3G或各种设备，如手机、平板电脑或台式计算机。

要设置ABR控制参数，请执行以下操作：

* 在上设置参数 `ABRControlParameters` 类。
