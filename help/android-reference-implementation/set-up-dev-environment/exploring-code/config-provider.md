---
description: ConfigProvider类获取媒体播放器的配置。 您必须实现配置接口，以便功能管理者能够读取配置信息。
seo-description: ConfigProvider类获取媒体播放器的配置。 您必须实现配置接口，以便功能管理者能够读取配置信息。
seo-title: 配置提供程序
title: 配置提供程序
uuid: 2467a617-6413-4b5d-9710-894cdc751b26
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# ConfigProvider {#configprovider}

ConfigProvider类获取媒体播放器的配置。 您必须实现配置接口，以便功能管理者能够读取配置信息。

使用[ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html)类实现`ICCConfig`、`IAAConfig`、`IPlaybackConfig`、`IAdConfig`和`IQosConfig`配置接口，以便功能管理器可以读取配置。 例如，`ICCConfig`是`CCManager`配置的接口。 配置文件从JSON配置文件接收配置参数。

`ConfigProvider.java`文件是Adobe实现配置接口的示例。 它从存储配置的`SharedPreferences`读取设置。 您可以以任何适合您的组织的方式存储配置。 配置实现为配置源提供一个包装器。