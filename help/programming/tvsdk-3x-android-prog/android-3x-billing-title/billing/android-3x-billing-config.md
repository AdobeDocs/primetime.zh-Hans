---
description: 如果您使用默认配置，则无需执行任何其他操作即可启用或配置计费。 如果您从Adobe启用代表获得了不同的配置参数，请在初始化媒体播放器之前使用BillingMetricsConfiguration类设置这些参数。
title: 配置计费量度
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# 配置帐单量度{#configure-billing-metrics}

如果您使用默认配置，则无需执行任何其他操作即可启用或配置计费。 如果您从Adobe启用代表获得了不同的配置参数，请在初始化媒体播放器之前使用BillingMetricsConfiguration类设置这些参数。

>[!TIP]
>
>大多数客户应使用默认配置。

>[!IMPORTANT]
>
>您设置的配置在媒体播放器的生命周期内保持有效。 初始化媒体播放器后，便无法更改配置。

要配置开单量度：

输入以下代码示例。

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
