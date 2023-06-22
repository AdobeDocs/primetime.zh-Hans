---
description: 如果您使用默认配置，则无需执行其他操作即可启用或配置计费。 如果您从Adobe启用代表处获取了不同的配置参数，请在初始化媒体播放器之前使用BillingMetricsConfiguration类设置这些参数。
title: 配置计费量度
exl-id: 1eb50822-77a0-4b3a-a84c-b6082bcd1cad
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 配置计费量度{#configure-billing-metrics}

如果您使用默认配置，则无需执行其他操作即可启用或配置计费。 如果您从Adobe启用代表处获取了不同的配置参数，请在初始化媒体播放器之前使用BillingMetricsConfiguration类设置这些参数。

大多数客户应使用默认配置。

>[!IMPORTANT]
>
>您设置的配置将在媒体播放器的生命周期内保持有效。 初始化媒体播放器后，无法更改配置。

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

   位置 `_player` 的实例 `AdobePSDK.MediaPlayer` 和 `_resource` 的实例 `AdobePSDK.MediaResource`.
