---
description: 可以使用PTSDKConfig类在TVSDK中全局配置自定义标记名称。
seo-description: 可以使用PTSDKConfig类在TVSDK中全局配置自定义标记名称。
seo-title: 标记的配置类方法
title: 标记的配置类方法
uuid: 27f1df0a-bbd3-4d80-820e-b659f2f33069
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 标记的配置类方法 {#config-class-methods-for-tags}

可以使用PTSDKConfig类在TVSDK中全局配置自定义标记名称。

TVSDK会自动将全局配置应用于任何未指定流特定配置的媒体流。

`PTSDKConfig` 显示这些方法以管理自定义标记：

| **订阅特定的自定义标记** |  |
|---|---|
| `subscribedTags` | 检索订阅标记的当前列表。 |
| `setSubscribedTags` | 设置将向应用程序公开的订阅标记列表。 |
| **自定义默认业务机会检测器使用的广告标记** |
| `adTags` | 检索广告标记的当前列表。 |
| `setAdTags` | 设置默认业务机会生成器将使用的广告标记列表。 |


请记住以下事项：

* setter方法不允许标记参数包含null值。
* 自定义标记名称必须包含#前缀。

   例如，#EXT-X-ASSET是正确的自定义标记名称，但EXT-X-ASSET不正确。
* 加载媒体流后，无法更改配置。