---
description: 您可以使用MediaPlayerItemConfig类在TVSDK中全局配置自定义标记名称。
title: 标记的配置类方法
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# 标记的配置类方法 {#config-class-methods-for-tags}

您可以使用MediaPlayerItemConfig类在TVSDK中全局配置自定义标记名称。

TVSDK会自动将全局配置应用于未指定流特定配置的任何媒体流。

`MediaPlayerItemConfig` 公开这些方法以管理自定义标记：

**订阅特定的自定义标记**

| <b>方法</b> | <b>描述</b> |
|--- |--- |
| `public final String[] getSubscribedTags` | 检索当前订阅的标记列表。 |
| `public final void setSubscribedTags(String[] tags);` | 设置将向应用程序公开的订阅标记的列表。  您的应用程序还会自动订阅通过传输的所有标记 `setAdTags`. |

**自定义默认机会检测器使用的广告标记**

| <b>方法</b> | <b>描述</b> |
|--- |--- |
| `public final String[] getAdTags;` | 检索当前的广告标记列表。 |
| `public final void setAdTags(String[] tags);` | 设置默认机会生成器将使用的广告标记列表。 |

请记住以下内容：

* setter方法不允许tags参数包含null值。

  如果遇到，TVSDK会引发 `IllegalArgumentException`.
* 自定义标记名称必须包含 `#` 前缀。

  例如， `#EXT-X-ASSET` 是正确的自定义标记名称，但 `EXT-X-ASSET` 不正确。

* 加载媒体流后，无法更改配置。
