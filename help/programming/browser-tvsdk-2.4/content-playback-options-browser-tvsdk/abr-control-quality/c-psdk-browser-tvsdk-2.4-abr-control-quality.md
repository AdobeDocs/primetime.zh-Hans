---
description: HLS和DASH流为同一短视频突发提供不同的比特率编码（配置文件）。 浏览器TVSDK可以根据可用带宽为每个突发数选择质量级别。
seo-description: HLS和DASH流为同一短视频突发提供不同的比特率编码（配置文件）。 浏览器TVSDK可以根据可用带宽为每个突发数选择质量级别。
seo-title: 视频质量的自适应比特率(ABR)
title: 视频质量的自适应比特率(ABR)
uuid: 4c34fb7b-1bbd-4fa9-8929-d50e85a17396
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 概述 {#adaptive-bit-rates-abr-for-video-quality-overview}

HLS和DASH流为同一短视频突发提供不同的比特率编码（配置文件）。 浏览器TVSDK可以根据可用带宽为每个突发数选择质量级别。

浏览器TVSDK会持续监视比特率，以确保内容以当前网络连接的最佳比特率播放。

您可以为多位速率(MBR)流设置自适应比特率(ABR)切换策略和初始、最小和最大比特率。 浏览器TVSDK会自动切换到在指定配置中提供最佳播放体验的位速率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始位速率 </td> 
   <td colname="col2">第一段的所需回放位速率（以位／秒为单位）。 当播放开始时，第一段使用等于或大于初始比特率的最近配置文件。 <p> 如果定义了最小比特率，并且初始比特率低于最小速率，则浏览器TVSDK选择具有高于最小比特率的最低比特率的配置文件。 如果初始速率高于最大速率，则浏览器TVSDK会选择低于最大速率的最高速率。 </p> <p>如果初始比特率为零或未定义，则初始比特率由ABR策略确定。 </p> <p><span class="codeph"> initialBitRate返回一个整数值，它表示每秒字节的配置文件。</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最低位速率 </td> 
   <td colname="col2">ABR可切换到的允许的最低位速率。 ABR切换会忽略比特率低于此比特率的配置文件。 <p><span class="codeph"> minBitRate返回一个整数值</span> ，它表示每秒的位配置文件。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2">ABR可切换到的允许的最高比特率。 ABR切换会忽略比特率高于此比特率的配置文件。 <p><span class="codeph"> maxBitRate返回一个整数值</span> ，它表示每秒的位数配置文件。 </p> </td> 
  </tr> 
 </tbody> 
</table>

请牢记以下信息：

* 当比特率发生更改时，Browser TVSDK将 `AdobePSDK.ProfileEvent` 调度类型为 `AdobePSDK.PSDKEventType.PROFILE_CHANGED`。

* 您可以随时更改ABR设置，播放器会切换为使用与最近设置最接近的配置文件。

例如，如果流具有以下配置文件：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果指定的范围是300000到20000000，则Browser TVSDK仅考虑配置文件1、2和3。 这使应用程序能够适应各种网络条件，如从wi-fi切换到3G或切换到手机、平板电脑或台式计算机等各种设备。

要设置ABR控制参数，请执行以下操作：

* 设置类的参 `ABRControlParameters` 数。

