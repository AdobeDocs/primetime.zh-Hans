---
description: 可以使用PTSDKConfig类在TVSDK中全局配置自定义标记名称。
seo-description: 可以使用PTSDKConfig类在TVSDK中全局配置自定义标记名称。
seo-title: 标记的配置类方法
title: 标记的配置类方法
uuid: 1d3651a0-3b70-4d3a-8ced-663a9dad7205
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# 标记{#config-class-methods-for-tags}的配置类方法

可以使用PTSDKConfig类在TVSDK中全局配置自定义标记名称。

TVSDK会自动将全局配置应用于任何未指定流特定配置的媒体流。

`PTSDKConfig` 显示以下用于管理自定义标记的方法：

| **订阅特定自定义标记** |
|---|
| `subscribedTags` | 检索订阅标记的当前列表。 |
| `setSubscribedTags` | 设置将向应用程序公开的订阅标记的列表。 |
| **自定义默认机会检测器使用的广告标记** |
| `adTags` | 检索广告标记的当前列表。 |
| `setAdTags` | 设置默认业务机会生成器将使用的广告标记的列表。 |

请记住以下事项：

* setter方法不允许标记参数包含null值。
* 自定义标记名称必须包含#前缀。

   例如，#EXT-X-ASSET是正确的自定义标记名称，但EXT-X-ASSET不正确。
* 加载媒体流后，无法更改配置。

