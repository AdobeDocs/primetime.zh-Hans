---
description: 如果您使用默认配置，则无需执行任何其他操作即可启用或配置计费。 如果您从“Adobe启用”代表处获取了不同的配置参数，请在初始化媒体播放器之前使用BillingMetricsConfiguration类设置这些参数。
title: 配置计费量度
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 配置计费量度 {#configure-billing-metrics}

如果您使用默认配置，则无需执行任何其他操作即可启用或配置计费。 如果您从“Adobe启用”代表处获取了不同的配置参数，请在初始化媒体播放器之前使用BillingMetricsConfiguration类设置这些参数。

>[!TIP]
>
>大多数客户应使用默认配置。

>[!IMPORTANT]
>
>您设置的配置将在媒体播放器的生命周期内保持有效。 初始化媒体播放器后，便无法更改配置。

要配置计费指标，请执行以下操作：

1. 输入以下代码示例。

   ```java
   MediaPlayerItemConfig config = new MediaPlayerItemConfig(); 
   BillingMetricsConfiguration billingConfig = new BillingMetricsConfiguration(); 
   billingConfig.setEnabled(true); 
   billingConfig.setProVODBillableDurationMinutes(60); 
   billingConfig.setStdVODBillableDurationMinutes(30); 
   billingConfig.setLiveBillableDurationMinutes(15); 
   config.setBillingMetricsConfiguration(billingConfig); 
   mediaPlayer.replaceCurrentResource(mediaResource, config);
   ```
