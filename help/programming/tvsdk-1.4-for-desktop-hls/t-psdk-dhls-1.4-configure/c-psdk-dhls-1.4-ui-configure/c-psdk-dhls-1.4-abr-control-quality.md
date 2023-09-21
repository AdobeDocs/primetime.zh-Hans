---
description: HLS和DASH流为相同的短突发视频提供不同的比特率编码（配置文件）。 TVSDK可以根据可用带宽选择每个突发的质量级别。
title: 用于视频质量的自适应比特率(ABR)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---

# 用于视频质量的自适应比特率(ABR){#adaptive-bit-rates-abr-for-video-quality}

HLS和DASH流为相同的短突发视频提供不同的比特率编码（配置文件）。 TVSDK可以根据可用带宽选择每个突发的质量级别。

TVSDK会持续监控比特率，以确保在当前网络连接中以最佳比特率播放内容。

您可以设置自适应比特率(ABR)切换策略以及多比特率(MBR)流的初始、最小和最大比特率。 TVSDK会自动切换到在指定配置中提供最佳播放体验的比特率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始比特率 </td> 
   <td colname="col2"> <p>第一段所需的播放比特率（位/秒）。 开始播放时，第一个区段使用最接近的配置文件，该配置文件等于或大于初始比特率。 </p> <p> 如果定义了最小比特率，并且初始比特率低于最小比特率，则TVSDK选择最低比特率高于最小比特率的配置文件。 如果初始速率高于最大速率，TVSDK将选择低于最大速率的最高速率。 </p> <p>如果初始比特率为零或未定义，则初始比特率由ABR策略确定。 </p> <p> <span class="apiname"> ABRIinitialBitRate </span> 返回表示每秒字节配置文件的整数值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小比特率 </td> 
   <td colname="col2"> <p>ABR可切换的最低允许比特率。 ABR切换将忽略比特率低于此比特率的配置文件。 </p> <p> <span class="apiname"> Abriminbitrate </span> 返回表示每秒位配置文件的整数值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2"> <p>ABR可切换的最高允许比特率。 ABR切换将忽略比特率高于此比特率的配置文件。 </p> <p> <span class="apiname"> ABRMaxBitRate </span> 返回表示每秒位配置文件的整数值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR切换策略 </td> 
   <td colname="col2"> 如果可能，播放将逐渐切换到最高比特率配置文件。 您可以设置ABR切换策略，该策略可决定TVSDK在配置文件之间切换的速度。 默认为 <span class="codeph"> MODERATE_POLICY </span>. <p>当TVSDK决定切换到更高的比特率时，播放器根据当前ABR策略选择理想的比特率配置文件以切换到： 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> 保守策略 </span>：当带宽比当前比特率高50%时，切换到具有下一更高比特率的配置文件。 </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> MODERATE_POLICY </span>：当带宽比当前比特率高20%时，切换到下一个更高的比特率配置文件。 </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> 主动策略 </span>：当带宽高于当前比特率时，立即切换到最高比特率配置文件。 </li> 
     </ul> </p> <p>如果初始比特率为零或未指定，但指定了策略，则播放开始时将采用最低比特率配置文件进行保守，采用最接近可用配置文件中间比特率的配置文件进行中度播放，采用最高比特率的配置文件进行激进。 </p> <p>如果指定了最小和最大比特率，则该策略将在约束下工作。 </p> <p> <span class="codeph"> ABRP政策 </span> 返回当前设置，从 <span class="codeph"> ABRControlParameters </span> 枚举：CONSERVATIVE_POLICY、MODERATE_POLICY或AGGRESSIVE_POLICY。 </p> </td> 
  </tr> 
 </tbody> 
</table>

请牢记以下信息：

* TVSDK故障转移机制可能会覆盖您的设置，因为TVSDK更倾向于持续播放体验，而不是严格遵守控制参数。
* 当比特率发生更改时，TVSDK将调度 `ProfileEvent.PROFILE_CHANGED`.
* 您可以随时更改ABR设置，播放器将切换为使用与最新设置最匹配的配置文件。

例如，如果流具有以下配置文件：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果指定300000到2000000的范围，TVSDK将仅考虑用户档案1、2和3。 这允许应用程序适应各种网络条件，例如从wi-fi切换到3G或各种设备，如手机、平板电脑或台式计算机。

要设置ABR控制参数，请执行下列操作之一：

* 使用 `ABRControlParameterBuilder` 帮助程序类来设置参数的任意子集(运行 `ABRControlParameter` 幕后)

* 在上设置参数 `ABRControlParameter` 类。

## 使用ABRControlParametersBuilder配置自适应比特率 {#section_3DDE397A7CE445E1832EBAA46CE5C069}

使用 `ABRControlParametersBuilder` helper类是设置ABR参数的最简单、最有效的方式。

* 此 `ABRControlParametersBuilder` 构造函数将所有ABR参数设置为基础上的默认值 `ABRControlParameters` 对象。

* 您可以在运行时重置单个ABR参数，只要保持对它的引用即可 `ABRControlParametersBuilder` 实例。

此类还包含 `toABRControlParameters()` 帮助程序方法。 使用此方法获取实例 `ABRControlParameters` 并将其设置在 `mediaPlayer.ABRControlParameters` 属性。 这会使您的设置在播放器中生效。

1. 实例化 `ABRControlParametersBuilder` 帮助程序类中，并在媒体播放器中设置参数。

   >[!NOTE]
   >
   >例如，下面的示例将所有参数初始化为默认值，然后仅将策略设置为保守值，并将最大比特率限制为1000000：
   >
   >```
   >var abrBuilder:ABRControlParametersBuilder =  
   >   new ABRControlParametersBuilder(); 
   >abrBuilder.policy = ABRControlParameters.CONSERVATIVE_POLICY; 
   >abrBuilder.maxBitRate = 1000000; 
   >mediaPlayer.abrControlParameters =  
   >   abrBuilder.toABRControlParameters();
   >```
   >

1. 在运行时修改单个ABR参数。

   要修改各个参数，同时保留其余参数，请执行以下操作：

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   要保留以前的设置，必须维护对它的引用 `ABRControlParametersBuilder` 您在步骤1中创建的实例。

## 使用ABRControlParameters配置自适应比特率 {#section_02161FD0A73F40ED9CAE17F9AF850483}

只能通过以下方式设置ABR控制值 `ABRControlParameters`，但您可以随时构建一个新的扩展。

在存在之前支持设置ABR参数的功能 `ABRControlParametersBuilder` 类，但此功能对于在构建时设置ABR参数仍然有效。 但是，要在构建后更改各个参数，您应使用 `ABRControlParametersBuilder` 类。

下列条件适用于 `ABRControlParameters`：

* 必须在构造时提供所有参数的值。
* 构造时间之后不能更改单个值。
* 如果指定的参数在允许的范围之外，则 `ArgumentError` 被抛出。

1. 决定初始、最小和最大比特率。
1. 确定ABR策略：

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. 将ABR参数值设置为 `ABRControlParameters` 构造函数并将其分配给媒体播放器。

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```
