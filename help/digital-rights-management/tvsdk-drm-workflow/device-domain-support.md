---
description: 通常，创建时所有Primetime DRM许可证都绑定到唯一设备。 此绑定可防止用户在不经授权的情况下跨不同设备共享许可证。 除了按设备绑定之外，Primetime DRM还提供将许可证绑定到设备域或设备组的能力。
seo-description: 通常，创建时所有Primetime DRM许可证都绑定到唯一设备。 此绑定可防止用户在不经授权的情况下跨不同设备共享许可证。 除了按设备绑定之外，Primetime DRM还提供将许可证绑定到设备域或设备组的能力。
seo-title: 使用域支持播放加密内容
title: 使用域支持播放加密内容
uuid: 8854cc0f-9bfc-4833-82d7-a3f46ac88e06
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 设备域支持 {#device-domain-support}

通常，创建时所有Primetime DRM许可证都绑定到唯一设备。 此绑定可防止用户在不经授权的情况下跨不同设备共享许可证。 除了按设备绑定之外，Primetime DRM还提供将许可证绑定到设备域或设备组的能力。

如果内容元数据指定需要设备域注册，则应用程序可以调用API加入设备组。 此操作会触发要发送到域服务器的域注册请求。 向设备组发放许可证后，可以导出许可证并与已加入设备组的其他设备共享许可证。

然后，设备组信息被用在对 `DRMContentData``VoucherAccessInfo` 象中，然后，该设备组信息将用于提供成功检索和使用许可证所需的信息。

## 使用域支持播放加密内容 {#play-encrypted-content-using-domain-support}

要使用Primetime DRM播放加密内容，请执行以下步骤：

1. 使用 `VoucherAccessInfo.deviceGroup`时，检查是否需要注册设备组。
1. 如果需要身份验证：
   1. 使用属 `DeviceGroupInfo.authenticationMethod` 性找出是否需要身份验证。
   1. 如果需要身份验证，请通过执行以下步骤之一验证用户身份：

      * 获取用户的用户名和密码并调用 `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`。
      * 获取缓存／预生成的身份验证令牌并调用 `DRMManager.setAuthenticationToken()`。
   1. 调用 `DRMManager.addToDeviceGroup()`
1. 通过执行下列任务之一获取内容的许可证：
   1. 使用方 `DRMManager.loadVoucher()` 法。
   1. 从在同一设备组中注册的其他设备获取许可证，并通过该方法向 ` DRMManager` 提供许 `DRMManager.storeVoucher()` 可证。
1. 使用该方法播放加密的 `Primetime.play()` 内容。
要导出内容的许可证，任何设备在从Primetime DRM许可证服务器获得许可证后，都可以使用该方 `DRMVoucher.toByteArray()` 法提供许可证的原始字节。 内容提供者通常限制设备组中的设备数量。 如果达到此限制，则可能需要在未使用的设备上调 `DRMManager.removeFromDeviceGroup()` 用该方法，然后注册当前设备。