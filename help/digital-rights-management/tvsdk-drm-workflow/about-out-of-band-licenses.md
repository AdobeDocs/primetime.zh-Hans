---
title: 带外许可证概述
description: 带外许可证概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# 带外许可证 {#out-of-band-licenses}

还可通过以下方式在带外（不联系Primetime DRM许可证服务器）获取许可证：使用将许可证存储在磁盘和内存中 `storeVoucher()` 方法。

要在Primetime中播放加密的视频，相应的运行时需要获得该视频的许可证。 许可证包含视频的解密密钥，由客户部署的Primetime DRM许可证服务器生成。

运行时通常通过将许可证请求发送到视频的DRM元数据( `DRMContentData` 类)。 应用程序可以通过调用 `DRMManager.loadVoucher()` 方法。

`DRMManager.storeVoucher()` 允许应用程序发送其已获得的带外许可证。 然后，运行时可以跳过许可证请求进程，并使用转发的许可证播放加密的视频。 在带外获取许可证之前，仍需要由Primetime DRM许可证服务器生成许可证。 但是，您可以选择将许可证托管在任何HTTP服务器上，而不是Primetime DRM许可证服务器上。

`DRMManager.storeVoucher()` 还用于支持多台设备之间的许可证共享。 在Primetime DRM 3.0之后，此功能称为“设备域支持”。 如果您的部署支持此用例，则可以使用将多台计算机注册到一个设备组 `DRMManager.addToDeviceGroup()` 方法。 如果某台计算机具有给定内容的有效域绑定许可证，则应用程序可以使用 `DRMVoucher.toByteArray()` 方法，并且您可在其他计算机上，使用 `DRMManager.storeVoucher()` 方法。

## 关于设备注册 {#about-device-registration}

所有Primetime DRM许可证在创建时都必须绑定到最终实体。 绑定是仅允许特定实体能够使用许可证的加密过程。 这是防止任何任意设备都可以使用的“浮动许可证”所必需的。 对于Primetime DRM“预生成”许可证，这意味着必须提前知道这些预生成许可证的“目标”。 Primetime DRM将此称为“设备注册”。

## 注册设备 {#register-a-device}

假设您已执行以下任务：

* 您已设置Primetime DRM服务器SDK。
* 您已经设置了HTTP服务器来颁发预生成的许可证。
* 您已创建一个Primetime应用程序来查看受保护的内容。

 设备注册阶段涉及以下操作：

1. 应用程序会创建一个随机生成的ID。
1. 应用程序调用 `DRMManager.authenticate()` 方法。 应用程序必须在身份验证请求中包含随机生成的ID。 例如，在用户名字段中包含ID。
1. 步骤2中提到的操作将导致Primetime DRM向客户服务器发送身份验证请求。 此请求包括设备证书：
   1. 服务器从请求中提取设备证书和生成的ID并存储。
   1. 客户子系统预生成此设备证书的许可证，存储这些许可证并以将其与生成的ID关联的方式授予对这些证书的访问权限。.
1. 服务器使用“success”消息响应请求。
1. 应用程序存储生成的ID。

在设备注册之后，应用程序会使用生成的ID，其使用方式与之前方案中使用设备ID的方式相同：
1. 应用程序将尝试查找生成的ID。
1. 如果找到生成的ID，应用程序将在下载预生成的许可证时使用生成的ID。 应用程序将许可证发送到Primetime DRM客户端以供使用 `DRMManager.storeVoucher()` 方法。.
1. 如果未找到生成的ID，应用程序将执行设备注册过程。

## DRM出厂重置 {#drm-factory-reset}

当设备的用户调用DRM出厂重置选项时，将清除设备证书。 要继续播放受保护的内容，应用程序必须再次完成设备注册过程。 如果应用程序发送过时的预生成许可证，则Primetime DRM客户端将拒绝该许可证，因为该许可证是针对旧设备ID加密的。

* FlashAPI： [DRMManager.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers()) - （只能调用以响应某些不可恢复的DRM错误代码。）
* iOS API： [DRManager resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* Android API： [DRMManager.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))
