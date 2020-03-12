---
description: 如果您使用默认配置，则无需执行任何其他操作即可启用或配置计费。 如果您从Adobe Enablement Representative获得了不同的配置参数，请在初始化媒体播放器之前使用BillingMetricsConfiguration类设置这些参数。
seo-description: 如果您使用默认配置，则无需执行任何其他操作即可启用或配置计费。 如果您从Adobe Enablement Representative获得了不同的配置参数，请在初始化媒体播放器之前使用BillingMetricsConfiguration类设置这些参数。
seo-title: 配置计费指标
title: 配置计费指标
uuid: 04d3b53e-f08c-49d0-ba42-5375f1307d2e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 配置计费指标{#configure-billing-metrics}

如果您使用默认配置，则无需执行任何其他操作即可启用或配置计费。 如果您从Adobe Enablement Representative获得了不同的配置参数，请在初始化媒体播放器之前使用BillingMetricsConfiguration类设置这些参数。

大多数客户应使用默认配置。

>[!IMPORTANT]
>
>您设置的配置在媒体播放器的生命周期中保持有效。 初始化媒体播放器后，便无法更改配置。

要配置计费指标，请执行以下操作：

* 输入以下代码示例。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.billingMetricsConfiguration.isEnabled = true; 
   config.billingMetricsConfiguration.proVODBillableDurationMinutes = 60; 
   config.billingMetricsConfiguration.stdVODBillableDurationMinutes = 30; 
   config.billingMetricsConfiguration.liveBillableDurationMinutes = 15; 
   _player.replaceCurrentResource(_resource, config);
   ```

   其中 `_player` 是实例 `AdobePSDK.MediaPlayer` 和 `_resource` 实例 `AdobePSDK.MediaResource`。

