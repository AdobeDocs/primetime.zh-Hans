---
description: 通常，创建时所有Primetime DRM许可证都绑定到唯一的设备。 此绑定可防止用户未经授权在不同设备之间共享许可证。 除了按设备绑定之外，Primetime DRM还提供将许可证绑定到设备域或设备组的功能。
title: 使用域支持播放加密内容
exl-id: 3c9badfc-046b-4c56-bde1-7b3b708bfaa2
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 设备域支持{#device-domain-support}

通常，创建时所有Primetime DRM许可证都绑定到唯一的设备。 此绑定可防止用户未经授权在不同设备之间共享许可证。 除了按设备绑定之外，Primetime DRM还提供将许可证绑定到设备域或设备组的功能。

如果内容元数据指定需要设备域注册，则应用程序可以调用API以加入设备组。 此操作会触发要发送到域服务器的域注册请求。 向设备组颁发许可证后，即可导出该许可证并与已加入设备组的其他设备共享该许可证。

然后，设备组信息将用在`DRMContentData` `VoucherAccessInfo`对象中，该对象随后将用于显示成功检索和使用许可证所需的信息。

## 使用域支持{#play-encrypted-content-using-domain-support}播放加密内容

要使用Primetime DRM播放加密内容，请执行以下步骤：

1. 使用`VoucherAccessInfo.deviceGroup`检查是否需要设备组注册。
1. 如果需要身份验证：
   1. 使用`DeviceGroupInfo.authenticationMethod`属性可确定是否需要身份验证。
   1. 如果需要验证，请通过执行以下步骤之一来验证用户：

      * 获取用户的用户名和密码并调用`DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`。
      * 获取缓存/预生成的身份验证令牌并调用`DRMManager.setAuthenticationToken()`。
   1. 调用`DRMManager.addToDeviceGroup()`
1. 执行以下任务之一，以获取内容的许可证：
   1. 使用`DRMManager.loadVoucher()`方法。
   1. 从在同一设备组中注册的其他设备获取许可证，并通过`DRMManager.storeVoucher()`方法将许可证提供给`DRMManager`。
1. 使用`Primetime.play()`方法播放加密内容。
要导出内容的许可证，任何设备在从Primetime DRM许可证服务器获得许可证后，都可以使用`DRMVoucher.toByteArray()`方法提供许可证的原始字节。 内容提供商通常会限制设备组中的设备数量。 如果达到限制，则您可能需要在注册当前设备之前，在未使用的设备上调用`DRMManager.removeFromDeviceGroup()`方法。
