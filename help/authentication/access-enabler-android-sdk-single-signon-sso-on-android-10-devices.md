---
title: 在Android 10应用程序上访问启用程序Android SDK单点登录(SSO)
description: 在Android 10应用程序上访问启用程序Android SDK单点登录(SSO)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---



# 在Android 10应用程序上访问启用程序Android SDK单点登录(SSO) {#access-enabler-android-sdk-single-sign-on-sso-on-android-10-apps}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 概述

在使用Android OS的设备上，可通过Access Enabler Android SDK使用Adobe Primetime身份验证支持的应用程序之间的单点登录(SSO)。 为了在Android设备上提供单点登录(SSO),Access Enabler Android SDK版本3.2.1（最新版本）及更早版本使用在Android存储实施中保存的共享数据库文件，所有支持Adobe Primetime身份验证的应用程序均可访问该文件。

但是，在最新的Android 10版本中，Google做出了一些更改，“以便让用户更好地控制其文件并限制文件混乱，默认情况下，面向Android 10（API级别29）及更高版本的应用程序可以获得外部存储设备（或范围存储）的范围访问权限。 此类应用程序只能看到其特定于应用程序的目录 `\[...\]`&quot; 有关这些Android 10存储更改的更多详细信息，请参阅 [适用于Android的数据和文件存储文档](https://developer.android.com/training/data-storage/files/external-scoped).

由于这些更改，Access Enabler Android版本提供的单点登录(SSO)发生了变化 **3.2.1 SDK（最新版）** 和以前版本可能会在Android 10设备上受到影响，如下一节中所述。

请参阅 [Roku SSO概述](/help/authentication/roku-sso-overview.md).

## 行为

具体取决于您应用程序的 **target SDK级别** 或 **android:requestLegacyExternalStorage** 清单属性Access Enabler Android 3.2.1 SDK（最新版本）及更早版本提供的单点登录(SSO)当前的行为如下所示：

- 您的应用程序目标 **Android 9（API级别28）** 或 **-\>** 单点登录(SSO) **会奏效**
- 您的应用程序目标 **Android 10** **（API级别29）** 和 **set** 的值 **requestLegacyExternalStorage设置为true** 在应用程序的清单文件中 **-\>** 单点登录(SSO) **会奏效**
- 您的应用程序目标 **Android 10** **（API级别29）** 和 **未设置** 的值 **requestLegacyExternalStorage设置为true** 在应用程序的清单文件中 **-\>** 单点登录(SSO) **不起作用**


>[!TIP]
>
> 在Adobe Primetime身份验证Access Enabler Android SDK与范围存储完全兼容之前，您可以根据应用程序的目标SDK级别或requestLegacyExternalStorage清单属性（如公共中所述）临时选择禁用 [Android文档](https://developer.android.com/training/data-storage/files/external-scoped#opt-out-of-scoped-storage).

