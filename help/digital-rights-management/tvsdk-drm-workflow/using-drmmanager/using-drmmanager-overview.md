---
title: 使用DRMManager类概述
description: 使用DRMManager类概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# 使用DRMManager类 {#using-the-drmmanager-class}

使用 `DRMManager` 类以管理应用程序中的许可证和Primetime DRM许可证服务器会话。

**许可证管理**

每当设备播放受保护的内容时，运行时都会获取并缓存查看内容所需的许可证。 如果应用程序将内容保存在本地，并且许可证允许离线播放，则用户无需网络连接即可查看应用程序中的内容。 使用 `DRMManager`中，您可以预缓存许可证。 应用程序不必获得查看内容所需的许可证。 例如，您的应用程序可以下载媒体文件，然后在用户仍然在线时获取许可证。

要预载许可证，请使用 `DRMContentData` 对象。 此 `DRMContentData` 对象包含可以提供许可证的Primetime DRM许可证服务器的URL，并描述是否需要用户身份验证。 利用这些信息，您可以调用 `DRMManager` `loadVoucher()` 获取并缓存许可证的方法。 有关预加载许可证的工作流的详细说明，请参阅 *为离线播放预加载许可证*.

**会话管理**

您也可以使用 `DRMManager` 向Primetime DRM许可证服务器验证用户身份，并管理持续会话。 调用 `DRMManager` `authenticate()` 与Primetime DRM许可证服务器建立会话的方法。 成功完成身份验证后， `DRMManager` 调度 `DRMAuthenticationCompleteEvent` 对象。 此对象包含一个会话令牌。 您可以保存此令牌以建立未来的会话，这样用户就不必提供其帐户凭据。 将令牌传递到 `setAuthenticationToken()` 用于建立新的经过身份验证的会话的方法。 （生成令牌的服务器的设置决定令牌过期及其他属性）。

## 处理DRMStatus事件 {#handling-drmstatus-events}

此 `DRMManager` 调度 `DRMStatusEvent` 调用后的对象 `loadVoucher()` 方法成功完成。 如果获得了许可证，则event对象的detail属性的值为： `DRM.voucherObtained`，并且优惠券属性包含 `DRMVoucher` 对象。 如果未获得许可证，则detail属性的值仍然为： `DRM.voucherObtained`；但是， voucher属性为空。 例如，如果您使用 `LoadVoucherSetting` 之 `localOnly` 并且没有本地缓存的许可证。 如果 `loadVoucher()` 调用未成功完成，可能是由于身份验证或通信错误，然后 `DRMManager` 调度 `DRMErrorEvent` 或 `DRMAuthenticationErrorEvent` 对象。

## 处理DRMAuthenticationComplete事件{#handling-drmauthenticationcomplete-events}

此 `DRMManager` 调度 `DRMAuthenticationCompleteEvent` 对象。 `authenticate()` 方法。 此 `DRMAuthenticationCompleteEvent` 对象包含一个可重复使用的令牌，该令牌可用于跨应用程序会话保留用户身份验证。 将此令牌传递到 `DRMManager` `setAuthenticationToken()` 重新建立会话的方法。 (令牌创建者设置令牌属性，例如过期。 Adobe不提供用于检查令牌属性的API。)

## 处理DRMAuthenticationError事件{#handling-drmauthenticationerror-events}

此 `DRMManager` 调度 `DRMAuthenticationErrorEvent` 对象。 `authenticate()` 或 `setAuthenticationToken()` 方法。
