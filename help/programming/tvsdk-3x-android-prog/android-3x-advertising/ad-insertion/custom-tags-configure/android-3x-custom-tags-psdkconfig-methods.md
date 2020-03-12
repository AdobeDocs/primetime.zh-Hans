---
description: 您可以使用MediaPlayerItemConfig类在TVSDK中全局配置自定义标记名称。
seo-description: 您可以使用MediaPlayerItemConfig类在TVSDK中全局配置自定义标记名称。
seo-title: 标记的配置类方法
title: 标记的配置类方法
uuid: b75aebac-4b94-4c42-bed4-3c17ad989cd1
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 标记的配置类方法 {#config-class-methods-for-tags}

您可以使用MediaPlayerItemConfig类在TVSDK中全局配置自定义标记名称。

TVSDK会自动将全局配置应用于任何未指定流特定配置的媒体流。

`MediaPlayerItemConfig` 显示这些方法以管理自定义标记：

**订阅特定的自定义标记**

| <b>方法</b> | <b>说明</b> |
|--- |--- |
| `public final String[] getSubscribedTags` | 检索订阅标记的当前列表。 |
| `public final void setSubscribedTags(String[] tags);` | 设置将向应用程序公开的订阅标记列表。  您的应用程序还会自动订阅通过传输的所有标签 `setAdTags`。 |

**自定义默认业务机会检测器使用的广告标记**

| <b>方法</b> | <b>说明</b> |
|--- |--- |
| `public final String[] getAdTags;` | 检索广告标记的当前列表。 |
| `public final void setAdTags(String[] tags);` | 设置默认业务机会生成器将使用的广告标记列表。 |

请记住以下事项：

* setter方法不允许标记参数包含null值。

   如果遇到，TVSDK将引发 `IllegalArgumentException`。
* 自定义标记名称必须包含前 `#` 缀。

   例如，自定 `#EXT-X-ASSET` 义标记名称正确，但 `EXT-X-ASSET` 不正确。

* 加载媒体流后，无法更改配置。