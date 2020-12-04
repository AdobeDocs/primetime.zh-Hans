---
description: HLS和DASH流为同一短视频突发提供不同的比特率编码(用户档案)。 TVSDK可以根据可用带宽为每个突发选择质量级别。
seo-description: HLS和DASH流为同一短视频突发提供不同的比特率编码(用户档案)。 TVSDK可以根据可用带宽为每个突发选择质量级别。
seo-title: 视频质量的自适应比特率(ABR)
title: 视频质量的自适应比特率(ABR)
uuid: e3d5ef90-067d-48e0-a025-081de931d842
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 0%

---


# 视频质量的自适应比特率(ABR){#adaptive-bit-rates-abr-for-video-quality}

HLS和DASH流为同一短视频突发提供不同的比特率编码(用户档案)。 TVSDK可以根据可用带宽为每个突发选择质量级别。

TVSDK会持续监视比特率，以确保以当前网络连接的最佳比特率播放内容。

可以为多比特率(MBR)流设置自适应比特率(ABR)切换策略以及初始、最小和最大比特率。 TVSDK自动切换到在指定配置中提供最佳播放体验的比特率。

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 初始比特率 </td> 
   <td colname="col2"> <p>第一段的所需回放位速率（以位／秒为单位）。 当播放开始时，对于第一段使用等于或大于初始比特率的最接近用户档案。 </p> <p> 如果定义了最小比特率，并且初始比特率低于最小速率，则TVSDK选择具有高于最小比特率的最低比特率的用户档案。 如果初始速率高于最大速率，则TVSDK将选择低于最大速率的最高速率。 </p> <p>如果初始比特率为零或未定义，则初始比特率由ABR策略确定。 </p> <p> <span class="apiname"> ABRInitialBitRate </span> 返回一个整数值，它表示每秒字节用户档案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最小比特率 </td> 
   <td colname="col2"> <p>ABR可以切换到的允许的最低比特率。 ABR切换忽略比特率低于此比特率的用户档案。 </p> <p> <span class="apiname"> ABRMinBitRate </span> 返回一个整数值，它表示每秒位用户档案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 最大比特率 </td> 
   <td colname="col2"> <p>ABR可以切换到的允许的最高比特率。 ABR切换忽略比特率高于此比特率的用户档案。 </p> <p> <span class="apiname"> ABRMaxBitRate </span> 返回一个整数值，它表示每秒的位用户档案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR切换策略 </td> 
   <td colname="col2"> 回放功能会尽可能逐渐切换到最高比特率的用户档案。 您可以设置ABR切换策略，该策略确定TVSDK在用户档案之间切换的速度。 默认值为<span class="codeph"> MEDEATE_POLICY </span>。 <p>当TVSDK决定切换到更高的比特率时，播放器会根据当前的ABR策略选择理想的比特率用户档案来切换： 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> CONSERVAL_POLICY  </span>:当带宽比当前比特率高50%时，切换到用户档案，其下一个比特率更高。 </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> MEDEATE_POLICY  </span>:当带宽比当前比特率高20%时，切换到下一个较高的比特率用户档案。 </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> ACCORSIVE_POLICY  </span>:当带宽高于当前比特率时，立即切换到最高比特率用户档案。 </li> 
     </ul> </p> <p>如果初始比特率为零或未指定，但指定了策略，则播放开始的比特率用户档案最低（保守），最接近中等可用用户档案的中位比特率的用户档案，以及攻击性的最高比特率用户档案。 </p> <p>如果指定了这些速率，则策略在最小比特率和最大比特率的约束下有效。 </p> <p> <span class="codeph"> ABRPolicy从 </span> ABRControlParameters枚举中返 <span class="codeph"> 回当前 </span> 设置：CONSERVAL_POLICY、MEATE_POLICY或ACCORSIVE_POLICY。 </p> </td> 
  </tr> 
 </tbody> 
</table>

请记住以下信息：

* TVSDK故障切换机制可能会覆盖您的设置，因为TVSDK更青睐连续播放体验，而不是严格遵循您的控制参数。
* 当比特率发生更改时，TVSDK将调度`ProfileEvent.PROFILE_CHANGED`。
* 您可以随时更改ABR设置，播放器会切换为使用与最近设置最接近的用户档案。

例如，如果流具有以下用户档案:

* 1:300000
* 2:700000
* 3:1500000
* 4:2400000
* 5:4000000

如果指定的范围是3000000到20000000，则TVSDK仅考虑用户档案1、2和3。 这使应用程序能够适应各种网络条件，如从wi-fi切换到3G或切换到手机、平板电脑或台式计算机等各种设备。

要设置ABR控制参数，请执行下列操作之一：

* 使用`ABRControlParameterBuilder`帮助类设置任何参数子集（在场景后的`ABRControlParameter`上操作）

* 设置`ABRControlParameter`类的参数。

## 使用ABRControlParametersBuilder {#section_3DDE397A7CE445E1832EBAA46CE5C069}配置自适应比特率

使用`ABRControlParametersBuilder`帮助类是设置ABR参数的最简单、最有效的方法。

* `ABRControlParametersBuilder`构造函数将所有ABR参数设置为基础`ABRControlParameters`对象的默认值。

* 只要保持对同一`ABRControlParametersBuilder`实例的引用，就可以在运行期间重置单个ABR参数。

此类还包括`toABRControlParameters()`帮助程序方法。 使用此方法获取`ABRControlParameters`的实例，并在`mediaPlayer.ABRControlParameters`属性上设置它。 这会使您的设置在播放器中生效。

1. 实例化`ABRControlParametersBuilder`帮助程序类，并在Media Player上设置参数。

   >[!NOTE]
   >
   >例如，以下示例将所有参数初始化为默认值，然后仅将策略设置为保守，并将最大比特率限制为1000000:
   >
   >
   ```
   >var abrBuilder:ABRControlParametersBuilder =  
   >   new ABRControlParametersBuilder(); 
   >abrBuilder.policy = ABRControlParameters.CONSERVATIVE_POLICY; 
   >abrBuilder.maxBitRate = 1000000; 
   >mediaPlayer.abrControlParameters =  
   >   abrBuilder.toABRControlParameters();
   >```

1. 在运行时修改单个ABR参数。

   在保留其余参数的同时修改各个参数：

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   要保留之前的设置，必须保留对您在步骤1中创建的同一`ABRControlParametersBuilder`实例的引用。

## 使用ABRControlParameters {#section_02161FD0A73F40ED9CAE17F9AF850483}配置自适应比特率

您只能用`ABRControlParameters`设置ABR控件值，但可以随时构建一个新值。

在存在`ABRControlParametersBuilder`类之前，支持设置ABR参数的功能，但此功能对于在构建时设置ABR参数仍然有效。 但是，要在构建后更改单个参数，应使用`ABRControlParametersBuilder`类。

以下条件适用于`ABRControlParameters`:

* 必须在构造时为所有参数提供值。
* 在构建时间后，不能更改单个值。
* 如果指定的参数超出允许的范围，则引发`ArgumentError`。

1. 确定初始、最小和最大比特率。
1. 确定ABR策略：

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. 在`ABRControlParameters`构造函数中设置ABR参数值，并将它们分配给Media Player。

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```

