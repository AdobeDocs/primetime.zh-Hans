---
title: 使用DRMManager类概述
description: 使用DRMManager类概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# 使用DRMManager类{#using-the-drmmanager-class}

使用`DRMManager`类管理应用程序中的许可证和Primetime DRM许可证服务器会话。

**许可证管理**

每当设备播放受保护的内容时，运行时获取并缓存视图内容所需的许可证。 如果应用程序将内容保存在本地，且许可证允许脱机回放，则用户无需网络连接即可在应用程序中视图内容。 使用`DRMManager`可以预缓存许可证。 应用程序不必获得视图内容所需的许可。 例如，您的应用程序可以下载媒体文件，然后在用户仍在线时获得许可证。

要预载许可证，请使用`DRMContentData`对象。 `DRMContentData`对象包含Primetime DRM许可证服务器的URL，该服务器可以提供许可证并描述是否需要用户身份验证。 利用此信息，您可以调用`DRMManager` `loadVoucher()`方法来获取和缓存许可证。 *脱机回放的预加载许可证*&#x200B;中更详细地介绍了预加载许可证的工作流程。

**会话管理**

您还可以使用`DRMManager`验证用户对Primetime DRM许可证服务器的身份，并管理永久会话。 调用`DRMManager` `authenticate()`方法与Primetime DRM许可证服务器建立会话。 成功完成身份验证后，`DRMManager`将调度`DRMAuthenticationCompleteEvent`对象。 此对象包含会话令牌。 您可以保存此令牌以建立将来的会话，这样用户就不必提供其帐户凭据。 将令牌传递给`setAuthenticationToken()`方法以建立新的已验证会话。 （生成令牌的服务器的设置决定令牌过期和其他属性）。

## 处理DRMStatus事件{#handling-drmstatus-events}

在对`loadVoucher()`方法的调用成功完成后，`DRMManager`将调度`DRMStatusEvent`对象。 如果获得许可证，则事件对象的detail属性具有以下值：`DRM.voucherObtained`, and the voucher property contains the `DRMVoucher` object. 如果未获得许可证，则detail属性仍具有以下值：`DRM.voucherObtained`;但是，voucher属性为null。 例如，如果您使用`localOnly`的`LoadVoucherSetting`，并且没有本地缓存的许可证，则无法获取许可证。 如果`loadVoucher()`调用未成功完成（可能是由于身份验证或通信错误），则`DRMManager`将调度`DRMErrorEvent`或`DRMAuthenticationErrorEvent`对象。

## 处理DRMAuthenticationComplete事件{#handling-drmauthenticationcomplete-events}

当用户通过调用`authenticate()`方法成功验证身份时，`DRMManager`将调度`DRMAuthenticationCompleteEvent`对象。 `DRMAuthenticationCompleteEvent`对象包含可重用的令牌，可用于跨应用程序会话保持用户身份验证。 将此令牌传递给`DRMManager` `setAuthenticationToken()`方法以重新建立会话。 (令牌创建器设置令牌属性，如过期。 Adobe不提供用于检查令牌属性的API。)

## 处理DRMAuthenticationError事件{#handling-drmauthenticationerror-events}

当用户无法通过调用`authenticate()`或`setAuthenticationToken()`方法成功验证时，`DRMManager`将调度`DRMAuthenticationErrorEvent`对象。