---
description: 通常，所有Primetime DRM许可证在创建时都绑定到唯一设备。 此绑定可防止用户在未经授权的情况下跨不同设备共享许可证。 除了按设备绑定，Primetime DRM还提供将许可证绑定到设备域或设备组的功能。
title: 使用域支持播放加密的内容
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 设备域支持 {#device-domain-support}

通常，所有Primetime DRM许可证在创建时都绑定到唯一设备。 此绑定可防止用户在未经授权的情况下跨不同设备共享许可证。 除了按设备绑定，Primetime DRM还提供将许可证绑定到设备域或设备组的功能。

如果内容元数据指定需要设备域注册，则应用程序可以调用API以加入设备组。 此操作会触发要发送到域服务器的域注册请求。 将许可证颁发给设备组后，可以导出许可证并与已加入设备组的其他设备共享。

然后，设备组信息将用于 `DRMContentData` `VoucherAccessInfo` 对象，然后用于提供成功检索和使用许可证所需的信息。

## 使用域支持播放加密的内容 {#play-encrypted-content-using-domain-support}

要使用Primetime DRM播放加密的内容，请执行以下步骤：

1. 使用 `VoucherAccessInfo.deviceGroup`，检查是否需要注册设备组。
1. 如果需要进行身份验证：
   1. 使用 `DeviceGroupInfo.authenticationMethod` 属性，了解是否需要身份验证。
   1. 如果需要进行身份验证，请执行以下步骤之一来验证用户：

      * 获取用户的用户名和密码并调用 `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`.
      * 获取缓存/预生成的身份验证令牌并调用 `DRMManager.setAuthenticationToken()`.

   1. 调用 `DRMManager.addToDeviceGroup()`
1. 通过执行以下任务之一获取内容的许可证：
   1. 使用 `DRMManager.loadVoucher()` 方法。
   1. 从同一设备组中注册的其他设备获取许可证，并将许可证提供给 `DRMManager` 通过 `DRMManager.storeVoucher()` 方法。
1. 使用播放加密的内容 `Primetime.play()` 方法。
要导出内容的许可证，任何设备都可以使用 `DRMVoucher.toByteArray()` 一种从Primetime DRM许可证服务器获取许可证的方法。 内容提供商通常会限制设备组中的设备数量。 如果达到限制，您可能需要调用 `DRMManager.removeFromDeviceGroup()` 注册当前设备之前在未使用的设备上的方法。
