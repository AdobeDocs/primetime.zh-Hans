---
title: Primetime 发行说明
description: Primetime 发行说明
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 28%

---


# Primetime 发行说明

欢迎阅读Adobe Primetime发行说明。 左侧导航中列出的文档提供特定于发行版的信息、系统要求、限制、已修复问题和已知问题。

## PTAI 21.2.2中的增强和修复

该版本包括对HLS流中EXT-X-IMAGE-STREAM-INF流插入/同步的支持。 此功能通过服务器端配置启用。 请联系您的技术客户代表以启用该功能。

## TVSDK 3.13 Android中的修复

此版本为解决FireTV设备(包括Fire TV第3代Sunte和Fire TV 多维数据集第1代和第2代设备)上Widevine DRM流冻结或显示ABR开关上的黑帧的问题提供了解决方法。

要解决此问题，请在启动播放之前为指定的Fire TV设备设置API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)`。 默认值为false。

有关详细信息，请参阅[TVSDK for Android发行说明](../release-notes/tvsdk-3x-android.md)。

## TVSDK 3.12 iOS发行说明中的增强和修复

此版本侧重于解决客户的主要问题。

有关[iOS](../release-notes/tvsdk-3x-ios.md)的当前已发布版本的详细信息，请查看。

## 另请参阅

| 用户指南 | 说明 |
|--- |--- |
| [Primetime 编程帮助](/help/programming/home.md) | 让您可以学习在 Android 设备上使用 Java 以及在 iOS 设备上使用 Objective-C 开发应用程序和视频播放器。 |
| [Primetime迁移和转化帮助](/help/migration-guides/home.md) | 解释从现有 Primetime TVSDK Suite 到下一代套件的转换和迁移流程。 |
| [参考实施](/help/android-reference-implementation/home.md) | 帮助理解 TVSDK 并修改功能管理器以自定义您的个人播放器。 |
| [Primetime API参考](/help/reference/api-references.md) | 提供有关 TVSDK 函数、数据结构和其他编程结构的详细信息。 |
| [Digital Rights Management](/help/digital-rights-management/home.md) | 帮助您进一步了解Digital Rights Management(DRM)中的各种用户场景 |
| [Primetime Ad Insertion 帮助](/help/primetime-ad-insertion/home.md) | 解释如何通过在服务器上插入面向用户的动态广告来从内容获利，以及如何通过个性化广告吸引受众。 |
| [存档](https://helpx.adobe.com/primetime/archives.html) | 下载归档文档的PDF。 |

## 有用资源

* [了解Adobe Primetime](https://www.adobe.com/in/marketing/primetime.html)

* [并发监控](https://tve.helpdocsonline.com/concurrency-monitoring-introduction)

* [Primetime身份验证](https://tve.helpdocsonline.com/home)

* [Adobe Primetime DRM论坛](https://forums.adobe.com/community/adobe_access)

* [Adobe Primetime开发人员资源](https://www.adobe.com/devnet/primetime.html)
