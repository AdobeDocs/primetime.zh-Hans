---
description: HLS和DASH流为同一短视频突发提供不同的比特率编码(用户档案)。 TVSDK可以根据可用带宽为每个突发选择质量级别。
seo-description: HLS和DASH流为同一短视频突发提供不同的比特率编码(用户档案)。 TVSDK可以根据可用带宽为每个突发选择质量级别。
seo-title: 视频质量的自适应比特率(ABR)
title: 视频质量的自适应比特率(ABR)
uuid: a9b9a6a8-4098-4952-90e7-684e64800b3f
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# 视频质量{#adaptive-bit-rates-abr-for-video-quality}的自适应比特率(ABR)

HLS和DASH流为同一短视频突发提供不同的比特率编码(用户档案)。 TVSDK可以根据可用带宽为每个突发选择质量级别。

TVSDK会持续监视比特率，以确保以当前网络连接的最佳比特率播放内容。

可以为多比特率(MBR)流设置自适应比特率(ABR)切换策略以及初始、最小和最大比特率。 TVSDK自动切换到在指定配置中提供最佳播放体验的比特率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始比特率 </td> 
   <td colname="col2"> <p>第一段的所需回放位速率（以位／秒为单位）。 当播放开始时，对于第一段使用等于或大于初始比特率的最接近用户档案。 </p> <p> 如果定义了最小比特率，并且初始比特率低于最小速率，则TVSDK选择具有高于最小比特率的最低比特率的用户档案。 如果初始速率高于最大速率，则TVSDK将选择低于最大速率的最高速率。 </p> <p>如果初始比特率为零或未定义，则初始比特率由ABR策略确定。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小比特率 </td> 
   <td colname="col2"> <p>ABR可以切换到的允许的最低比特率。 ABR切换忽略比特率低于此比特率的用户档案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2"> <p>ABR可以切换到的允许的最高比特率。 ABR切换忽略比特率高于此比特率的用户档案。 </p> </td> 
  </tr> 
 </tbody> 
</table>

请记住以下信息：

* TVSDK不从比特率切换中调度事件。
* 您可以随时更改ABR设置，播放器会切换为使用与最近设置最接近的用户档案。

例如，如果流具有以下用户档案:

* 1:300000
* 2:700000
* 3:1500000
* 4:2400000
* 5:4000000

如果指定的范围是3000000到20000000，则TVSDK仅考虑用户档案1、2和3。 这使应用程序能够适应各种网络条件，如从WiFi切换到3G或切换到手机、平板电脑或台式计算机等各种设备。

## 配置自适应比特率{#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

要配置TVSDK自适应比特率参数：

1. 配置`PTABRControlParameters`的实例以设置初始、最小和最大比特率设置。

   默认值显示在以下代码片断中，但您的应用程序可以为每个这些参数设置任何整数值。

   >[!IMPORTANT]
   >
   >以位／秒(bps)为单位指定比特率设置。

   ```
   // ARC (add autorelease for non-ARC) 
   PTABRControlParameters *abrMetaData =  
       [[PTABRControlParameters alloc] init];  
   
   abrMetaData.initialBitRate = -1; 
   abrMetaData.minBitRate = 0; 
   abrMetaData.maxBitRate = INT_MAX;
   ```

1. 使用已配置的`PTABRControlParameters`实例更新您的`PTMediaPlayer`实例。

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

请记住以下事项：

* 应用程序必须先在`PTMediaPlayer`上设置`abrControlParameters`属性，然后才能配置`PTMediaPlayerItem`实例，初始和最小比特率设置才能生效。

   在内容播放开始后，设置新实例只会影响最大比特率设置。

* 要在播放期间更新最大比特率设置，请新建一个`PTABRControlParameters`实例，并在播放器实例上设置它。
* 您只能在iOS 8.0及更高版本上播放期间更新最大比特率设置。 对于早期版本，使用在内容播放开始之前设置的`maxBitrate`值。