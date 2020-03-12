---
description: HLS和DASH流为同一短视频突发提供不同的比特率编码（配置文件）。 TVSDK可以根据可用带宽为每个突发选择质量级别。
seo-description: HLS和DASH流为同一短视频突发提供不同的比特率编码（配置文件）。 TVSDK可以根据可用带宽为每个突发选择质量级别。
seo-title: 视频质量的自适应比特率(ABR)
title: 视频质量的自适应比特率(ABR)
uuid: e3d5ef90-067d-48e0-a025-081de931d842
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 视频质量的自适应比特率(ABR){#adaptive-bit-rates-abr-for-video-quality}

HLS和DASH流为同一短视频突发提供不同的比特率编码（配置文件）。 TVSDK可以根据可用带宽为每个突发选择质量级别。

TVSDK会持续监视比特率，以确保内容以当前网络连接的最佳比特率播放。

您可以为多位速率(MBR)流设置自适应比特率(ABR)切换策略和初始、最小和最大比特率。 TVSDK会自动切换到在指定配置中提供最佳播放体验的位速率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始位速率 </td> 
   <td colname="col2"> <p>第一段的所需回放位速率（以位／秒为单位）。 当播放开始时，第一段使用等于或大于初始比特率的最近配置文件。 </p> <p> 如果定义了最小比特率，并且初始比特率低于最小速率，则TVSDK选择具有高于最小比特率的最低比特率的配置文件。 如果初始速率高于最大速率，则TVSDK选择低于最大速率的最高速率。 </p> <p>如果初始比特率为零或未定义，则初始比特率由ABR策略确定。 </p> <p> <span class="apiname"> ABRInitialBitRate返 </span> 回一个表示每秒字节配置文件的整数值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最低位速率 </td> 
   <td colname="col2"> <p>ABR可切换到的允许的最低位速率。 ABR切换会忽略比特率低于此比特率的配置文件。 </p> <p> <span class="apiname"> ABRMinBitRate返 </span> 回一个表示每秒位数配置文件的整数值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2"> <p>ABR可切换到的允许的最高比特率。 ABR切换会忽略比特率高于此比特率的配置文件。 </p> <p> <span class="apiname"> ABRMaxBitRate返 </span> 回一个表示每秒位配置文件的整数值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR切换策略 </td> 
   <td colname="col2"> 如果可能，回放会逐渐切换到最高比特率的配置文件。 您可以设置ABR切换策略，该策略确定TVSDK在配置文件之间切换的速度。 默认值为 <span class="codeph"> MEADE_POLICY </span>。 <p>当TVSDK决定切换到更高的比特率时，播放器会根据当前的ABR策略选择理想的比特率配置文件以切换到： 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> CONSURACTIVE_POLICY </span>:当带宽比当前比特率高50%时，切换到具有下一个较高比特率的配置文件。 </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> MEADORE_POLICY </span>:当带宽比当前比特率高20%时，切换到下一个较高的比特率配置文件。 </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> ACCORVISE_POLICY </span>:当带宽高于当前比特率时，立即切换到最高比特率配置文件。 </li> 
     </ul> </p> <p>如果初始比特率为零或未指定，但指定了策略，则回放将从最低比特率配置文件（保守）开始，该配置文件最接近中等可用配置文件的中位速率配置文件，而最高比特率配置文件（侵略性）开始。 </p> <p>如果指定了这些速率，则策略在最小比特率和最大比特率的约束下有效。 </p> <p> <span class="codeph"> ABRPolicy从 </span> ABRControlParameters枚举返回当 <span class="codeph"> 前设 </span> 置：CONSERVACY_POLICY、MEATE_POLICY或ACCORSIVE_POLICY。 </p> </td> 
  </tr> 
 </tbody> 
</table>

请牢记以下信息：

* TVSDK故障转移机制可能会覆盖您的设置，因为TVSDK倾向于持续播放体验，而不是严格遵循您的控制参数。
* 当比特率发生更改时，TVSDK将调度 `ProfileEvent.PROFILE_CHANGED`。
* 您可以随时更改ABR设置，播放器会切换为使用与最近设置最接近的配置文件。

例如，如果流具有以下配置文件：

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

如果指定的范围是300000到20000000，则TVSDK只考虑配置文件1、2和3。 这使应用程序能够适应各种网络条件，如从wi-fi切换到3G或切换到手机、平板电脑或台式计算机等各种设备。

要设置ABR控制参数，请执行下列操作之一：

* 使用 `ABRControlParameterBuilder` 帮助类设置任何参数子集(在幕后 `ABRControlParameter` 操作)

* 设置类的参 `ABRControlParameter` 数。

## 使用ABRControlParametersBuilder配置自适应比特率 {#section_3DDE397A7CE445E1832EBAA46CE5C069}

使用 `ABRControlParametersBuilder` helper类是设置ABR参数最简单、最有效的方法。

* 构 `ABRControlParametersBuilder` 造函数将所有ABR参数设置为基础对象的默认 `ABRControlParameters` 值。

* 只要保持对同一实例的引用，就可以在运行期间重置单个ABR参 `ABRControlParametersBuilder` 数。

此类还包含帮助 `toABRControlParameters()` 程序方法。 使用此方法获取的实例 `ABRControlParameters` 并在属性中设置它 `mediaPlayer.ABRControlParameters` 。 这会使您的设置在播放器中生效。

1. 实例化 `ABRControlParametersBuilder` 帮助程序类，并在Media Player上设置参数。

   >[!NOTE]
   >
   >例如，下面的示例将所有参数初始化为默认值，然后将策略仅设置为保守，并将最大比特率限制为1000000:   >
   >
   >
   ```>
   >var abrBuilder:ABRControlParametersBuilder =  
   >   new ABRControlParametersBuilder(); 
   >abrBuilder.policy = ABRControlParameters.CONSERVATIVE_POLICY; 
   >abrBuilder.maxBitRate = 1000000; 
   >mediaPlayer.abrControlParameters =  
   >   abrBuilder.toABRControlParameters();
   >```   >
   >



1. 在运行时修改单个ABR参数。

   在保留其余参数的同时修改各个参数：

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   要保留之前的设置，您必须保留对您在步骤1中创 `ABRControlParametersBuilder` 建的同一实例的引用。

## 使用ABRControlParameters配置自适应比特率 {#section_02161FD0A73F40ED9CAE17F9AF850483}

您只能使用设置ABR控件值 `ABRControlParameters`，但可以随时构建一个新值。

在类存在之前，支持设置ABR参数的能力，但该能 `ABRControlParametersBuilder` 力对于在构造时设置ABR参数仍然有效。 但是，要在构建后更改单个参数，应使用类 `ABRControlParametersBuilder` 。

以下条件适用于 `ABRControlParameters`:

* 必须在构造时为所有参数提供值。
* 在构建时间后，不能更改单个值。
* 如果您指定的参数超出允许的范围，则会引 `ArgumentError` 发一个参数。

1. 确定初始、最小和最大比特率。
1. 确定ABR策略：

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. 在构造函数中设置ABR参 `ABRControlParameters` 数值，并将其分配给Media Player。

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```

