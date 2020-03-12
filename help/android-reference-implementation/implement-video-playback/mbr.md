---
description: TVSDK可以播放多个配置文件且位速率不同的视频，在它们之间切换以根据可用带宽提供多个质量级别。
seo-description: TVSDK可以播放多个配置文件且位速率不同的视频，在它们之间切换以根据可用带宽提供多个质量级别。
seo-title: 多比特率
title: 多比特率
uuid: 46eac41e-0b2a-42e3-8a88-54ad9fe34212
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 多比特率 {#multiple-bit-rates}

TVSDK可以播放多个配置文件且位速率不同的视频，在它们之间切换以根据可用带宽提供多个质量级别。

可以为多比特率(MBR)流设置初始、最小和最大比特率以及自适应比特率(ABR)切换策略。 TVSDK会自动切换到在指定配置内提供最佳播放体验的位速率。

引用实现在IPlaybackConfig中配置以下ABR [参数](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html)。

| 参数 | 说明 |
|--- |--- |
| 初始位速率： getABRInitialBitRate | 第一段的所需回放位速率（以位／秒为单位）。 当播放开始时，第一段使用最接近的配置文件（等于或大于初始位速率）。  如果定义了最小比特率并且初始比特率低于最小比特率，则TVSDK选择具有高于最小比特率的最低比特率的配置文件。 同样，如果初始速率高于最大速率，TVSDK将选择低于最大速率的最高速率。 如果初始比特率为零或未定义，则初始比特率由ABR策略确定。  返回一个整数值，它表示每秒的字节配置文件。 |
| 最小比特率： getABRMinBitRate | ABR可切换到的允许的最低位速率。 ABR切换会忽略比特率低于此的配置文件。 返回一个表示每秒位数配置文件的整数值。 |
| 最大比特率： getABRMaxBitRate | ABR可切换到的允许的最高比特率。 ABR切换会忽略比特率高于此的配置文件。 返回一个表示每秒位数配置文件的整数值。 |
| ABR切换策略： getABRPolicy | 如果可能，回放会逐渐切换到最高比特率的配置文件。 您可以设置ABR切换策略，该策略确定TVSDK在配置文件之间切换的速度。 默认值为“中等”。 <ul><li>*保守派*:当带宽比当前比特率高50%时，切换到具有下一个较高比特率的配置文件。 </li><li>*审核*:当带宽比当前比特率高20%时，切换到下一个较高的比特率配置文件。</li><li>*咄咄逼人*:当带宽高于当前比特率时，立即切换到最高比特率配置文件</li></ul><br/>如果初始比特率为零或未指定，并且指定了策略，则回放将从Consurative的最低比特率配置文件开始，该配置文件最接近Medeate的可用配置文件的中位速率配置文件，而Accorsive的最高比特率配置文件。<br/><br/>策略在最小和最大比特率的约束范围内工作（如果已指定）。  返回ABRControlParameters枚举的当前设置： <ul><li>ABR_CONSURACY</li><li>ABR_MEADE </li><li>ABR_ACCORSIVE</li></ul><br>另请参 [阅ABRPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/ABRControlParameters.ABRPolicy.html)。 |

>[!NOTE]
>
>* TVSDK故障转移机制可能会覆盖这些设置，因为TVSDK偏好持续播放体验，而不是严格遵守控制参数。
>* 当比特率发生更改时，TVSDK将在中 `onProfileChanged` 调度事件 `PlaybackEventListener`。


## 在参考实现中启用自定义ABR控制 {#section_72A6E7263E1441DD8D7E0690285515E6}

默认情况下，TVSDK中启用了自适应比特率(ABR)。 您可以通过配置自定义ABR控件，使用Primetime设置用户界面来覆盖参考实现中的默认TVSDK行为。

要通过“设置”用户界面启用自定义ABR，请执行以下操作：

* 打开“Primetime设置”对话框。
* 选择 **[!UICONTROL ABR controls]**。

   ![](assets/abr-configuration.jpg)

* 点按控 [!UICONTROL Enable ON] 件以显示该控 `OFF`件。

如 `PlaybackManager` 果isABRControlEnabled返回true [](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) (ON)，则仅设置ABR参数。 如果返回false(OFF)，则使用默 `PlaybackManager` 认的ABR控件，因此初始、最小和最大位速率都将为0，而ABR策略将为 `ABR_MODERATE`。

## 配置低位速率 {#section_5451691CBBD24542AD54A474D222CD39}

对于某些低位速率的播放速率，默认情况下，TVSDK会切换到纯音频流，并且播放会冻结。 您可以配置播放器，使其不会遇到切换为仅音频的情况。

* 实现 [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) 接口：

* 确保 [getABRMinBitRate](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#getABRMinBitRate()) 高于仅音频比特率（高于64000）。
* 确保 [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#isABRControlEnabled()) 打开。