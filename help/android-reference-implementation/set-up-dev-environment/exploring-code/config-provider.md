---
description: ConfigProvider类获取媒体播放器的配置。 您必须实施配置接口，以便功能管理器可以读取配置信息。
title: 配置提供程序
exl-id: 75613bfb-3c2b-4b53-b365-adc98f7e1164
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# 配置提供程序 {#configprovider}

ConfigProvider类获取媒体播放器的配置。 您必须实施配置接口，以便功能管理器可以读取配置信息。

您使用 [配置提供程序](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 类以实现 `ICCConfig`， `IAAConfig`， `IPlaybackConfig`， `IAdConfig`、和 `IQosConfig` 配置接口，以便功能管理器可以读取配置。 例如， `ICCConfig` 是的界面 `CCManager` 配置。 配置文件从JSON配置文件接收配置参数。

此 `ConfigProvider.java` file是Adobe配置接口实现的示例。 它从以下位置读取设置 `SharedPreferences`，其中存储了配置。 您可以采用适用于贵组织的任何方式来存储配置。 配置实施为您的配置源提供了一个包装器。
