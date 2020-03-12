---
seo-title: 使用DRMManager类概述
title: 使用DRMManager类概述
uuid: 71ce061b-75b6-4ab5-8bbd-cafe7c3e4592
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 使用DRMManager类 {#using-the-drmmanager-class}

使用该类 `DRMManager` 管理应用程序中的许可证和Primetime DRM许可证服务器会话。

**许可证管理**

每当设备播放受保护的内容时，运行时都会获取并缓存查看内容所需的许可证。 如果应用程序将内容保存在本地，并且许可证允许脱机回放，则用户无需网络连接即可在应用程序中查看内容。 使用 `DRMManager`可预缓存许可证。 应用程序不必获得查看内容所需的许可证。 例如，您的应用程序可以下载媒体文件，然后在用户仍在线时获取许可证。

要预载许可证，请使用对 `DRMContentData` 象。 该对 `DRMContentData` 象包含Primetime DRM许可证服务器的URL，该URL可以提供许可证并描述是否需要用户身份验证。 利用此信息，您可以调用该方 `DRMManager` 法来获 `loadVoucher()` 取和缓存许可证。 预加载许可证的工作流程在脱机回放的预加 *载许可证中有更详细的介绍*。

**会话管理**

您还可以使用该 `DRMManager` 用户对Primetime DRM许可证服务器进行身份验证并管理永久会话。 调用该 `DRMManager` 方法以 `authenticate()` 与Primetime DRM许可证服务器建立会话。 成功完成身份验证后，将 `DRMManager` 调度一个 `DRMAuthenticationCompleteEvent` 对象。 此对象包含会话令牌。 您可以保存此令牌以建立将来的会话，这样用户就不必提供其帐户凭据。 将令牌传递给方 `setAuthenticationToken()` 法以建立新的已验证会话。 （生成令牌的服务器的设置决定令牌的过期时间和其他属性）。

## 处理DRMStatus事件 {#handling-drmstatus-events}

对方 `DRMManager` 法的调 `DRMStatusEvent` 用成功完成后，将调 `loadVoucher()` 度对象。 如果获得了许可证，则事件对象的detail属性具有以下值： `DRM.voucherObtained`, and the voucher property contains the `DRMVoucher` object. 如果未获得许可证，则detail属性仍具有以下值： `DRM.voucherObtained`;但是，voucher属性为null。 例如，如果您使用的是，并且没有本地缓存的许 `LoadVoucherSetting` 可证， `localOnly` 则无法获取许可证。 如果调 `loadVoucher()` 用未成功完成（可能由于身份验证或通信错误），则调度 `DRMManager` 一个 `DRMErrorEvent` 或对 `DRMAuthenticationErrorEvent` 象。

## 处理DRMAuthenticationComplete事件{#handling-drmauthenticationcomplete-events}

当用 `DRMManager` 户通 `DRMAuthenticationCompleteEvent` 过调用该方法成功验证时，该对象调度 `authenticate()` 对象。 该对 `DRMAuthenticationCompleteEvent` 象包含可重用的令牌，可用于跨应用程序会话保持用户身份验证。 将此令牌传 `DRMManager` 递给方 `setAuthenticationToken()` 法以重新建立会话。 (令牌创建者设置令牌属性，如过期时间。 Adobe不提供用于检查令牌属性的API。)

## 处理DRMAuthenticationError事件{#handling-drmauthenticationerror-events}

当用 `DRMManager` 户无法通 `DRMAuthenticationErrorEvent` 过调用或方法成功验证身份时，该对象 `authenticate()` 将调度 `setAuthenticationToken()` 对象。