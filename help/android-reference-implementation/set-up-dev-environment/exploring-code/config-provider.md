---
description: ConfigProvider类获取媒体播放器的配置。 必须实施配置接口，以便功能管理器可以读取配置信息。
title: 配置提供程序
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# 配置提供程序 {#configprovider}

ConfigProvider类获取媒体播放器的配置。 必须实施配置接口，以便功能管理器可以读取配置信息。

您使用 [配置提供程序](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 类以实现 `ICCConfig`， `IAAConfig`， `IPlaybackConfig`， `IAdConfig`、和 `IQosConfig` 配置接口，以便功能管理器可以读取配置。 例如， `ICCConfig` 是的接口 `CCManager` 配置。 配置文件从JSON配置文件接收配置参数。

此 `ConfigProvider.java` 文件是Adobe实现配置界面的示例。 它会从以下位置读取设置 `SharedPreferences`：存储配置的位置。 您可以采用适合您组织的任何方式来存储配置。 配置实施为您的配置源提供了一个包装器。
