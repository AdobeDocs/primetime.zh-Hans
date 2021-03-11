---
description: TVSDK可以播放具有不同位速率的多个用户档案的视频，在它们之间切换，以根据可用带宽提供多个质量级别。
title: 多位速率
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---


# 多位速率{#multiple-bit-rates}

TVSDK可以播放具有不同位速率的多个用户档案的视频，在它们之间切换，以根据可用带宽提供多个质量级别。

可以设置初始、最小和最大比特率，以及多比特率(MBR)流的自适应比特率(ABR)切换策略。 TVSDK自动切换到在指定配置中提供最佳播放体验的比特率。

引用实现在[IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html)中配置以下ABR参数。

| 参数 | 说明 |
|--- |--- |
| 初始比特率： getABRInitialBitRate | 第一段的所需回放比特率（以位/秒为单位）。 当播放开始时，第一段使用最接近的用户档案（等于或大于初始比特率）。  如果定义了最小比特率并且初始比特率低于最小比特率，则TVSDK选择具有高于最小比特率的最低比特率的用户档案。 同样，如果初始速率高于最大速率，则TVSDK将选择低于最大速率的最高速率。 如果初始比特率为零或未定义，则初始比特率由ABR策略确定。  返回一个整数值，它表示每秒字节用户档案。 |
| 最低比特率： getABRMinBitRate | ABR可切换到的允许的最低位速率。 ABR切换会忽略比特率低于此的用户档案。 返回一个整数值，它表示每秒位用户档案。 |
| 最大比特率： getABRMaxBitRate | ABR可切换到的最高允许位速率。 ABR切换会忽略比特率高于此的用户档案。 返回一个整数值，它表示每秒位用户档案。 |
| ABR切换策略： getABRPolicy | 如果可能，回放将逐渐切换到最高位速率用户档案。 您可以设置ABR切换策略，该策略确定TVSDK在用户档案之间切换的速度。 默认为“中级”。 <ul><li>*保守*:当带宽比当前比特率高50%时，切换到具有下一个较高比特率的用户档案。 </li><li>*适中*:当带宽比当前比特率高20%时，切换到下一个较高的比特率用户档案。</li><li>*咄咄逼人*:当带宽高于当前比特率时，立即切换到最高比特率用户档案</li></ul><br/>如果初始位速率为零或未指定策略，则播放开始的比特率用户档案为Consurative最低，用户档案最接近Medore可用用户档案的中位速率，而Accorsive用户档案的比特率为最高。<br/><br/>策略在最小和最大比特率的限制内有效（如果已指定）。从ABRControlParameters枚举返回当前设置： <ul><li>ABR_CONSURAL</li><li>ABR_MEODE </li><li>ABR_ACCORSIVE</li></ul><br>另请参 [阅ABRPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/ABRControlParameters.ABRPolicy.html)。 |

>[!NOTE]
>
>* TVSDK故障转移机制可能会覆盖这些设置，因为TVSDK更青睐连续播放体验，而不是严格遵守控制参数。
>* 当位速率更改时，TVSDK在`PlaybackEventListener`中调度`onProfileChanged`事件。


## 在引用实现{#section_72A6E7263E1441DD8D7E0690285515E6}中启用自定义ABR控件

自适应比特率(ABR)默认在TVSDK中处于启用状态。 您可以通过配置自定义ABR控件，使用Primetime设置用户界面来覆盖参考实现中的默认TVSDK行为。

要通过“设置”用户界面启用自定义ABR，请执行以下操作：

* 打开“Primetime设置”对话框。
* 选择&#x200B;**[!UICONTROL ABR controls]**。

   ![](assets/abr-configuration.jpg)

* 点按[!UICONTROL Enable ON]控件，以便它显示`OFF`。

`PlaybackManager`仅在[isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html)返回true(ON)时设置ABR参数。 如果返回false(OFF),`PlaybackManager`将使用默认的ABR控件，因此初始、最小和最大比特率都将为0，而ABR策略将为`ABR_MODERATE`。

## 配置低位速率{#section_5451691CBBD24542AD54A474D222CD39}

对于某些低比特率的播放速率，默认情况下，TVSDK切换到纯音频流，并且播放显示冻结。 您可以配置播放器，使其不会遇到切换到纯音频的情况。

* 实现[ IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html)接口：

* 确保[getABRMinBitRate](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#getABRMinBitRate())高于纯音频比特率(高于64000)。
* 确保[isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#isABRControlEnabled())已打开。