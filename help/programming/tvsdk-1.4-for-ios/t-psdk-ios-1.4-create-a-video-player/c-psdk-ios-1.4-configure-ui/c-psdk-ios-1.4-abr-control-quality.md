---
description: HLS和DASH流为同一短突发视频提供不同的比特率编码（配置文件）。 TVSDK可以根据可用带宽选择每个突发的质量级别。
title: 用于视频质量的自适应比特率(ABR)
exl-id: dd6d091a-58c9-4825-8c2c-a1257ef37f22
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# 用于视频质量的自适应比特率(ABR){#adaptive-bit-rates-abr-for-video-quality}

HLS和DASH流为同一短突发视频提供不同的比特率编码（配置文件）。 TVSDK可以根据可用带宽选择每个突发的质量级别。

TVSDK会持续监控比特率，以确保内容以当前网络连接的最佳比特率播放。

您可以为多比特率(MBR)流设置自适应比特率(ABR)切换策略以及初始、最小和最大比特率。 TVSDK会自动切换到在指定配置中提供最佳播放体验的比特率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始比特率 </td> 
   <td colname="col2"> <p>第一段所需的播放比特率（以位/秒为单位）。 当播放开始时，第一个区段使用最接近的配置文件，该配置文件等于或大于初始比特率。 </p> <p> 如果定义了最小比特率，并且初始比特率低于最小比特率，则TVSDK选择最低比特率高于最小比特率的配置文件。 如果初始速率高于最大速率，TVSDK会选择低于最大速率的最高速率。 </p> <p>如果初始比特率为零或未定义，则初始比特率由ABR策略确定。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小比特率 </td> 
   <td colname="col2"> <p>ABR可切换的最低允许比特率。 ABR切换将忽略比特率低于此比特率的配置文件。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2"> <p>ABR可以切换到的允许的最高比特率。 ABR切换忽略比特率高于此比特率的配置文件。 </p> </td> 
  </tr> 
 </tbody> 
</table>

请牢记以下信息：

* TVSDK不会调度来自比特率切换的事件。
* 您可以随时更改ABR设置，播放器将切换为使用与最新设置最匹配的配置文件。

例如，如果流具有以下配置文件：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果指定300000到2000000的范围，TVSDK仅考虑用户档案1、2和3。 这允许应用程序适应各种网络条件，例如从WiFi切换到3G或各种设备，如手机、平板电脑或台式计算机。

## 配置自适应比特率 {#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

要配置TVSDK自适应比特率参数，请执行以下操作：

1. 配置实例 `PTABRControlParameters` 设置初始、最小和最大比特率设置。

   默认值显示在以下代码片段中，但您的应用程序可以为每个参数设置任意整数值。

   >[!IMPORTANT]
   >
   >以每秒位(bps)为单位指定比特率设置。

   ```
   // ARC (add autorelease for non-ARC) 
   PTABRControlParameters *abrMetaData =  
       [[PTABRControlParameters alloc] init];  
   
   abrMetaData.initialBitRate = -1; 
   abrMetaData.minBitRate = 0; 
   abrMetaData.maxBitRate = INT_MAX;
   ```

1. 更新您的 `PTMediaPlayer` 已配置的实例 `PTABRControlParameters` 实例。

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

请记住以下内容：

* 应用程序必须设置 `abrControlParameters` 属性 `PTMediaPlayer` 在配置之前 `PTMediaPlayerItem` 初始比特率和最小比特率设置的实例生效。

   内容播放开始后，设置新实例仅影响最大比特率设置。

* 要在播放期间更新最大比特率设置，请新建一个 `PTABRControlParameters` 实例并在播放器实例上设置它。
* 您只能在iOS 8.0及更高版本上的播放期间更新最大比特率设置。 对于早期版本，使用 `maxBitrate` 在使用内容播放之前设置的值。
