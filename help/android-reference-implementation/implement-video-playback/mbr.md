---
description: TVSDK可以播放多个用户档案且位速率不同的视频，在它们之间切换，以根据可用带宽提供多个质量级别。
seo-description: TVSDK可以播放多个用户档案且位速率不同的视频，在它们之间切换，以根据可用带宽提供多个质量级别。
seo-title: 多比特率
title: 多比特率
uuid: 46eac41e-0b2a-42e3-8a88-54ad9fe34212
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---


# 多比特率{#multiple-bit-rates}

TVSDK可以播放多个用户档案且位速率不同的视频，在它们之间切换，以根据可用带宽提供多个质量级别。

可以为多比特率(MBR)流设置初始、最小和最大比特率以及自适应比特率(ABR)切换策略。 TVSDK自动切换到在指定配置中提供最佳播放体验的比特率。

引用实现在[IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html)中配置以下ABR参数。

| 参数 | 说明 |
|--- |--- |
| 初始比特率： getABRInitialBitRate | 第一段的所需回放位速率（以位／秒为单位）。 当播放开始时，第一段使用最接近的用户档案（等于或大于初始比特率）。  如果定义了最小比特率并且初始比特率低于最小比特率，则TVSDK选择比特率低于最小比特率的用户档案。 同样，如果初始速率高于最大速率，TVSDK将选择低于最大速率的最高速率。 如果初始比特率为零或未定义，则初始比特率由ABR策略确定。  返回一个整数值，它表示每秒字节用户档案。 |
| 最小比特率： getABRMinBitRate | ABR可以切换到的允许的最低比特率。 ABR切换会忽略比特率低于此速率的用户档案。 返回一个整数值，它表示每秒的位用户档案。 |
| 最大比特率： getABRMaxBitRate | ABR可以切换到的允许的最高比特率。 ABR切换会忽略比特率高于此速率的用户档案。 返回一个整数值，它表示每秒的位用户档案。 |
| ABR切换策略： getABRPolicy | 如果可能，回放将逐渐切换到最高比特率用户档案。 您可以设置ABR切换策略，该策略确定TVSDK在用户档案之间切换的速度。 默认值为“中等”。 <ul><li>*保守派*:当带宽比当前比特率高50%时，切换到用户档案，其下一个比特率更高。 </li><li>*中等*:当带宽比当前比特率高20%时，切换到下一个较高的比特率用户档案。</li><li>*咄咄逼人*:当带宽高于当前比特率时，立即切换到最高比特率用户档案</li></ul><br/>如果初始比特率为零或未指定，并且指定了策略，则播放开始的比特率用户档案为Consurative最低，用户档案最接近中等可用用户档案的中位速率，而Accorsive用户档案的比特率最高。<br/><br/>策略在最小比特率和最大比特率的约束下工作（如果已指定）。从ABRControlParameters枚举返回当前设置： <ul><li>ABR_CONSURACY</li><li>ABR_MEDEATE </li><li>ABR_ACCORSIVE</li></ul><br>另请参 [阅ABRPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/ABRControlParameters.ABRPolicy.html)。 |

>[!NOTE]
>
>* TVSDK故障切换机制可能会覆盖这些设置，因为TVSDK更青睐连续播放体验，而不是严格遵守控制参数。
>* 当比特率发生变化时，TVSDK在`PlaybackEventListener`中调度`onProfileChanged`事件。


## 在参考实现{#section_72A6E7263E1441DD8D7E0690285515E6}中启用自定义ABR控制

自适应比特率(ABR)默认在TVSDK中处于启用状态。 您可以通过配置自定义ABR控件，使用Primetime设置用户界面来覆盖参考实现中的默认TVSDK行为。

要通过“设置”用户界面启用自定义ABR，请执行以下操作：

* 打开Primetime设置对话框。
* 选择&#x200B;**[!UICONTROL ABR controls]**。

   ![](assets/abr-configuration.jpg)

* 点按[!UICONTROL Enable ON]控件，以显示`OFF`。

`PlaybackManager`仅在[isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html)返回true(ON)时设置ABR参数。 如果返回false(OFF),`PlaybackManager`将使用默认的ABR控件，因此初始、最小和最大比特率都将为0，而ABR策略将为`ABR_MODERATE`。

## 配置低位速率{#section_5451691CBBD24542AD54A474D222CD39}

对于某些低比特率的播放速率，默认情况下，TVSDK会切换到纯音频流，并且播放显示冻结。 您可以配置播放器，使其不会遇到切换为纯音频的情况。

* 实现[IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html)接口：

* 确保[getABRMinBitRate](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#getABRMinBitRate())高于纯音频比特率（高于64000）。
* 确保[isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#isABRControlEnabled())已打开。