---
description: 功能管理器用作TVSDK库的包装。
seo-description: 功能管理器用作TVSDK库的包装。
seo-title: 参考实现结构
title: 参考实现结构
uuid: ae347a97-1500-476a-9fc8-c99e6b2ab8de
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# 参考实现结构{#reference-implementation-structure}

功能管理器用作TVSDK库的包装。

在Java中，类以层次结构化。 例如，`com.adobe.primetime.reference.ui`下的所有与UI相关的代码和所有功能管理器都位于`com.adobe.primetime.reference.manager`下。

Primetime参考实施包含以下包：

| 包 | 说明 |
|--- |--- |
| [com.adobe.primetime.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html) | 此类扩展android.app.Application。 |
| [com.adobe.primetime.reference.advertising](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html) | 包含自定义广告的代码。 |
| [com.adobe.primetime.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html) | 包含配置功能管理器所需的接口代码。 |
| [com.adobe.primetime.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html) | 包含DRM的辅助类。 |
| [com.adobe.primetime.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html) | 接口、平台和参考信息的适配器和物料适配器。 还包括FeedAdapterFactory、ContentRenditionInfo和XMLParserHelper代码。 |
| [com.adobe.primetime.reference.logging](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html) | 提供用于本地和远程记录的类。 |
| [com.adobe.primetime.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html) | 您可以在这里找到功能管理器和ManagerFactory。 对于可启用或禁用的可选功能，有两个功能管理器： <ul><li>一个功能管理器，即该功能的名称，例如CCManager。 此功能管理器已关闭，并提供默认关闭行为。</li><li>一个功能管理器，其在功能管理器名称中附加了“开”(On)，例如CCManagerOn。 此功能管理器为启用的功能提供示例代码。</li></ul> |
| [com.adobe.primetime.reference.ui.catalog](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html) | 包含目录的UI代码。 |
| [com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html) | 包含日志的UI代码。 |
| [com.adobe.primetime.reference.ui.player](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html) | 包含播放器的UI代码。 |
| [com.adobe.primetime.reference.ui.se设置](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html) | 包含设置的UI代码。 |
| [com.adobe.primetime.reference.utils](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html) | 包含一般实用程序类。 |
| [com.adobe.primetime.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html) | 包含`HTTP-specific`实用程序类。 |
