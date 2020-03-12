---
description: ConfigProvider类获取媒体播放器的配置。 必须实现配置界面，功能管理器才能读取配置信息。
seo-description: ConfigProvider类获取媒体播放器的配置。 必须实现配置界面，功能管理器才能读取配置信息。
seo-title: ConfigProvider
title: ConfigProvider
uuid: 2467a617-6413-4b5d-9710-894cdc751b26
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# ConfigProvider {#configprovider}

ConfigProvider类获取媒体播放器的配置。 必须实现配置界面，功能管理器才能读取配置信息。

您可以使 [用ConfigProvider类来实现](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 、 `ICCConfig`、 `IAAConfig``IPlaybackConfig`和配置界面，以便功能管理 `IAdConfig``IQosConfig` 器可以读取配置。 例如， `ICCConfig` 是配置的接 `CCManager` 口。 配置文件从JSON配置文件接收配置参数。

该 `ConfigProvider.java` 文件是Adobe实现配置界面的示例。 它从存储配 `SharedPreferences`置的位置读取设置。 您可以以任何适合您的组织的方式存储配置。 配置实现为配置源提供一个包装器。