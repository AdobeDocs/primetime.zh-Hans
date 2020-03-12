---
description: HLS和DASH流为同一短视频突发提供不同的比特率编码（配置文件）。 TVSDK可以根据可用带宽为每个突发选择质量级别。
seo-description: HLS和DASH流为同一短视频突发提供不同的比特率编码（配置文件）。 TVSDK可以根据可用带宽为每个突发选择质量级别。
seo-title: 视频质量的自适应比特率(ABR)
title: 视频质量的自适应比特率(ABR)
uuid: e5752d7e-fa7d-407c-96df-c3830a35c66e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 视频质量的自适应比特率(ABR){#adaptive-bit-rates-abr-for-video-quality}

HLS和DASH流为同一短视频突发提供不同的比特率编码（配置文件）。 TVSDK可以根据可用带宽为每个突发选择质量级别。

TVSDK会持续监视比特率，以确保内容以当前网络连接的最佳比特率播放。

您可以为多位速率(MBR)流设置自适应比特率(ABR)切换策略和初始、最小和最大比特率。 TVSDK会自动切换到在指定配置中提供最佳播放体验的位速率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始位速率 </td> 
   <td colname="col2"> <p>第一段的所需回放位速率（以位／秒为单位）。 当播放开始时，第一段使用等于或大于初始比特率的最近配置文件。 </p> <p> 如果定义了最小比特率，并且初始比特率低于最小速率，则TVSDK选择具有高于最小比特率的最低比特率的配置文件。 如果初始速率高于最大速率，则TVSDK选择低于最大速率的最高速率。 </p> <p>如果初始比特率为零或未定义，则初始比特率由ABR策略确定。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最低位速率 </td> 
   <td colname="col2"> <p>ABR可切换到的允许的最低位速率。 ABR切换会忽略比特率低于此比特率的配置文件。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2"> <p>ABR可切换到的允许的最高比特率。 ABR切换会忽略比特率高于此比特率的配置文件。 </p> </td> 
  </tr> 
 </tbody> 
</table>

请牢记以下信息：

* TVSDK不从比特率切换中调度事件。
* 您可以随时更改ABR设置，播放器会切换为使用与最近设置最接近的配置文件。

例如，如果流具有以下配置文件：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果指定的范围是300000到20000000，则TVSDK只考虑配置文件1、2和3。 这使应用程序能够适应各种网络条件，如从WiFi切换到3G或切换到手机、平板电脑或台式计算机等各种设备。

## 配置自适应比特率 {#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

要配置TVSDK自适应比特率参数，请执行以下操作：

1. 配置实例以 `PTABRControlParameters` 设置初始、最小和最大比特率设置。

   默认值显示在以下代码片断中，但您的应用程序可以为每个这些参数设置任何整数值。

   >[!IMPORTANT]
   >
   >以每秒位数(bps)为单位指定位速率设置。

   ```
   // ARC (add autorelease for non-ARC) 
   PTABRControlParameters *abrMetaData =  
       [[PTABRControlParameters alloc] init];  
   
   abrMetaData.initialBitRate = -1; 
   abrMetaData.minBitRate = 0; 
   abrMetaData.maxBitRate = INT_MAX;
   ```

1. 使用已配 `PTMediaPlayer` 置的实例更新您的 `PTABRControlParameters` 实例。

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

请记住以下事项：

* 应用程序必须先在 `abrControlParameters` 上设置属 `PTMediaPlayer` 性，然后才能 `PTMediaPlayerItem` 配置初始和最小比特率设置的实例。

   在内容播放开始后，设置新实例只影响最大比特率设置。

* 要在播放期间更新最大比特率设置，请创建一个 `PTABRControlParameters` 新实例，然后在播放器实例上设置它。
* 您只能在iOS 8.0和更高版本上播放期间更新最大比特率设置。 对于早期版本，将 `maxBitrate` 使用在内容播放开始之前设置的值。

