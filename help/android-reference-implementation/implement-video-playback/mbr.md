---
description: TVSDK可以播放具有不同比特率的多个配置文件的视频，在它们之间切换以根据可用带宽提供多个质量级别。
title: 多位速率
exl-id: 5f71d69e-993a-4985-accd-7ce2104f837e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# 多位速率 {#multiple-bit-rates}

TVSDK可以播放具有不同比特率的多个配置文件的视频，在它们之间切换以根据可用带宽提供多个质量级别。

您可以为多比特率(MBR)流设置初始比特率、最小比特率和最大比特率以及自适应比特率(ABR)切换策略。 TVSDK会自动切换到在指定配置中提供最佳播放体验的比特率。

参考实施会在中配置以下ABR参数 [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html).

| 参数 | 描述 |
|--- |--- |
| 初始比特率：getABRIinitialBitRate | 第一段所需的播放比特率（以位/秒为单位）。 当播放开始时，将最接近的配置文件（等于或大于初始比特率）用于第一个区段。  如果定义了最小比特率并且初始比特率低于最小比特率，则TVSDK选择最低比特率高于最小比特率的配置文件。 同样，如果初始速率高于最大速率，TVSDK会选择低于最大速率的最高速率。 如果初始比特率为零或未定义，则初始比特率由ABR策略确定。  返回表示每秒字节配置文件的整数值。 |
| 最小比特率： getABRMinBitRate | ABR可切换的最低允许比特率。 ABR切换将忽略比特率低于此的配置文件。 返回一个整数值，该值表示每秒位数的配置文件。 |
| 最大比特率： getABRMaxBitRate | ABR可以切换到的允许的最高比特率。 ABR切换会忽略比特率高于此的配置文件。 返回一个整数值，该值表示每秒位数的配置文件。 |
| ABR切换策略： getABRPolicy | 如果可能，播放将逐渐切换到最高比特率配置文件。 您可以设置ABR切换策略，以确定TVSDK在配置文件之间切换的速度。 默认值为“审核”。 <ul><li>*保守*：当带宽比当前比特率高50%时，切换到具有下一较高比特率的配置文件。 </li><li>*审核*：当带宽比当前比特率高20%时，切换到下一个更高的比特率配置文件。</li><li>*激进*：当带宽高于当前比特率时，立即切换到最高比特率配置文件</li></ul><br/>如果初始比特率为零或未指定策略并且指定了策略，则播放开始时会包括：对于Conservative为最低比特率配置文件；对于Moderate为最接近可用配置文件的中位比特率的配置文件；以及Aggressive为最高比特率配置文件。<br/><br/>如果指定最小和最大比特率的约束，则该策略将在约束范围内工作。  从ABRControlParameters枚举返回当前设置： <ul><li>ABR_保守</li><li>ABR_MODERATE </li><li>ABR_AGGRESSIVE</li></ul><br>另请参阅 [ABRP策略](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/ABRControlParameters.ABRPolicy.html). |

>[!NOTE]
>
>* TVSDK故障转移机制可能会覆盖这些设置，因为TVSDK更喜欢连续播放体验，而不是严格遵守控制参数。
>* 当比特率改变时，TVSDK调度 `onProfileChanged` 中的事件 `PlaybackEventListener`.


## 在参考实施中启用自定义ABR控制 {#section_72A6E7263E1441DD8D7E0690285515E6}

默认情况下，TVSDK中启用了自适应比特率(ABR)。 您可以通过配置自定义ABR控件，使用Primetime设置用户界面覆盖参考实施中的默认TVSDK行为。

要通过“设置”用户界面启用自定义ABR，请执行以下操作：

* 打开Primetime设置对话框。
* 选择 **[!UICONTROL ABR controls]**.

   ![](assets/abr-configuration.jpg)

* 点按 [!UICONTROL Enable ON] 控件，以便显示 `OFF`.

此 `PlaybackManager` 仅设置ABR参数，如果 [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) 返回true （开）。 如果返回false (OFF)，则 `PlaybackManager` 使用默认的ABR控制，因此初始、最小和最大比特率都将为0，而ABR策略将为 `ABR_MODERATE`.

## 配置低比特率 {#section_5451691CBBD24542AD54A474D222CD39}

对于某些低比特率播放，默认情况下，TVSDK会切换到纯音频流，并且播放似乎处于冻结状态。 您可以配置播放器，使其永远不会遇到切换到纯音频的情况。

* 实施 [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) 界面：

* 确保 [getabriminbitrate](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#getABRMinBitRate()) 高于纯音频比特率(高于64000)。
* 确保 [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#isABRControlEnabled()) 打开。
