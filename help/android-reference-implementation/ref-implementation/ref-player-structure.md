---
description: 功能管理器用作TVSDK库的包装器。
title: 参考实现结构
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# 参考实现结构 {#reference-implementation-structure}

功能管理器用作TVSDK库的包装器。

在Java中，类在层次结构中进行结构化。 例如，下的所有与用户界面相关的代码 `com.adobe.primetime.reference.ui` 并且所有功能管理器都位于 `com.adobe.primetime.reference.manager`.

Primetime引用实施包含以下包：

| 包 | 描述 |
|--- |--- |
| [com.adobe.primetime.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html) | 此类扩展android.app.Application。 |
| [com.adobe.primetime.reference.advertising](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html) | 包含自定义广告的代码。 |
| [com.adobe.primetime.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html) | 包含配置功能管理器所需的接口代码。 |
| [com.adobe.primetime.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html) | 包含DRM的帮助程序类。 |
| [com.adobe.primetime.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html) | 接口、平台和参考信息的适配器和项适配器。 还包括FeedAdapterFactory、ContentRenditionInfo和XMLParserHelper代码。 |
| [com.adobe.primetime.reference.logging](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html) | 提供用于本地和远程日志记录的类。 |
| [com.adobe.primetime.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html) | 您可以在此处找到功能管理器和ManagerFactory。 对于可以启用或禁用的可选功能，有两个功能管理器： <ul><li>一个功能管理器，它是功能的名称，例如CCManager。 此功能管理器已关闭，并提供默认关闭行为。</li><li>功能管理器名称后附加有On的功能管理器，例如CCManagerOn。 此功能管理器提供了已启用功能的示例代码。</li></ul> |
| [com.adobe.primetime.reference.ui.catalog](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html) | 包含目录的用户界面代码。 |
| [com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html) | 包含日志的用户界面代码。 |
| [com.adobe.primetime.reference.ui.player](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html) | 包含播放器的用户界面代码。 |
| [com.adobe.primetime.reference.ui.settings](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html) | 包含设置的用户界面代码。 |
| [com.adobe.primetime.reference.utils](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html) | 包含常规实用程序类。 |
| [com.adobe.primetime.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html) | 包含 `HTTP-specific` 实用程序类。 |
