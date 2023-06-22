---
title: Access Enabler Android 10应用程序上的Android SDK单点登录(SSO)
description: Access Enabler Android 10应用程序上的Android SDK单点登录(SSO)
exl-id: dedade15-c451-4757-b684-d3728e11dd87
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Access Enabler Android 10应用程序上的Android SDK单点登录(SSO) {#access-enabler-android-sdk-single-sign-on-sso-on-android-10-apps}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

## 概述

在使用Android操作系统的设备上，可通过Access Enabler Android SDK在Adobe Primetime身份验证支持的应用程序之间进行单点登录(SSO)。 为了在Android设备上提供单点登录(SSO)，Access Enabler Android SDK版本3.2.1（最新）及更早版本使用保存在Android存储实施中的共享数据库文件，所有Adobe Primetime身份验证支持的应用程序都可以访问。

但是，Google在最新的Android 10版本中做出了一些更改，“以便让用户更好地控制其文件并限制文件混乱，默认情况下，面向Android 10 （API级别29）及更高版本的应用程序将获得对外部存储设备或作用域存储的作用域访问权限。 此类应用程序只能查看其应用程序特定的目录 `\[...\]`“。 有关这些Android 10存储更改的更多详细信息，请参阅 [Android的数据和文件存储文档](https://developer.android.com/training/data-storage/files/external-scoped).

由于这些更改，Access Enabler Android版本提供了单点登录(SSO) **3.2.1 SDK（最新）** 和之前的版本可能会在Android 10设备上受到影响，具体情况见下一节中所述。

参见 [Roku SSO概述](/help/authentication/roku-sso-overview.md).

## 行为

根据您应用程序的 **目标SDK级别** 或使用 **android：requestLegacyExternalStorage** 清单属性Access Enabler Android版本3.2.1 SDK（最新）和先前版本提供的单一登录(SSO)当前行为如下所示：

- 您的应用程序目标 **Android 9（API级别28）** 或以下 **-\>** 单点登录(SSO) **将有效**
- 您的应用程序目标 **Android 10** **（API级别29）** 并且会 **设置** 的值 **requestLegacyExternalStorage设置为true** 在应用程序的清单文件中 **-\>** 单点登录(SSO) **将有效**
- 您的应用程序目标 **Android 10** **（API级别29）** 并且会 **未设置** 的值 **requestLegacyExternalStorage设置为true** 在应用程序的清单文件中 **-\>** 单点登录(SSO) **不起作用**


>[!TIP]
>
> 在Adobe Primetime Authentication Access Enabler Android SDK与作用域存储完全兼容之前，您可以根据应用程序的目标SDK级别或requestLegacyExternalStorage清单属性（如公开内容中所述）临时选择退出 [Android文档](https://developer.android.com/training/data-storage/files/external-scoped#opt-out-of-scoped-storage).
