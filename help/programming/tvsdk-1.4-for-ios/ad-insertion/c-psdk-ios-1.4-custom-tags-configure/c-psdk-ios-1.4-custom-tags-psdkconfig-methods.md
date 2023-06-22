---
description: 您可以使用PTSDKConfig类在TVSDK中全局配置自定义标记名称。
title: 标记的配置类方法
exl-id: b23bba25-ddab-4700-bae6-db1ee833eea2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 标记的配置类方法{#config-class-methods-for-tags}

您可以使用PTSDKConfig类在TVSDK中全局配置自定义标记名称。

TVSDK会自动将全局配置应用于未指定流特定配置的任何媒体流。

`PTSDKConfig` 显示以下方法以管理自定义标记：

| **订阅特定的自定义标记** |
|---|
| `subscribedTags` | 检索订阅标签的当前列表。 |
| `setSubscribedTags` | 设置将向应用程序公开的订阅标记的列表。 |
| **自定义默认机会检测器使用的广告标记** |
| `adTags` | 检索广告标记的当前列表。 |
| `setAdTags` | 设置默认机会生成器将使用的广告标记列表。 |

请记住以下内容：

* setter方法不允许tags参数包含null值。
* 自定义标记名称必须包含#前缀。

   例如，#EXT-X-ASSET是正确的自定义标记名称，但EXT-X-ASSET不正确。
* 加载媒体流后，无法更改配置。
