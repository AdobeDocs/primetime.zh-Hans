---
seo-title: 带外许可证概述
title: 带外许可证概述
uuid: 82e4529a-ee1b-4c0c-8885-e0e68319d1a0
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---


# 带外许可证{#out-of-band-licenses}

通过使用`storeVoucher()`方法将许可证存储在磁盘和内存中，也可获得带外许可证（无需联系Primetime DRM许可证服务器）。

要在Primetime中播放加密视频，相应的运行时需要获得该视频的许可证。 该许可证包含视频的解密密钥，由客户部署的Primetime DRM许可证服务器生成。

运行时通常通过向视频的DRM元数据（`DRMContentData`类）中指示的Primetime DRM许可证服务器发送许可证请求来获得此许可证。 应用程序可以通过调用`DRMManager.loadVoucher()`方法来触发此许可证请求。

`DRMManager.storeVoucher()` 允许应用程序发送其获得的带外许可证。然后，运行时可以跳过许可证请求过程，使用转发的许可证播放加密视频。 许可证仍需由Primetime DRM许可证服务器生成，才能在带外获得。 但是，您可以选择在任何HTTP服务器而不是Primetime DRM许可证服务器上存放许可证。

`DRMManager.storeVoucher()` 还用于支持多个设备之间的许可证共享。在Primetime DRM 3.0之后，此功能称为“设备域支持”。 如果您的部署支持此用例，则可以使用`DRMManager.addToDeviceGroup()`方法将多台计算机注册到设备组。 如果某台计算机具有针对特定内容的有效域绑定许可证，则应用程序随后可以使用`DRMVoucher.toByteArray()`方法提取序列化许可证，而在您的其他计算机上，您可以使用`DRMManager.storeVoucher()`方法导入许可证。

## 关于设备注册{#about-device-registration}

创建时，所有Primetime DRM许可证都必须绑定到最终实体。 绑定是仅允许特定实体使用许可证的加密过程。 这对于防止任何任意设备都可以使用的“浮动许可证”是必要的。 对于Primetime DRM要“预生成”许可证，这意味着这些预生成许可证的“目标”必须提前知道。 Primetime DRM称之为“设备注册”。

## 注册设备{#register-a-device}

假定您已执行以下任务:

* 您已设置Primetime DRM Server SDK。
* 您已设置一个HTTP服务器，用于发放预生成的许可证。
* 您已创建了一个Primetime应用程序来视图受保护的内容。

 设备注册阶段涉及以下操作：

1. 应用程序会创建随机生成的ID。
1. 应用程序调用`DRMManager.authenticate()`方法。 应用程序必须在身份验证请求中包含随机生成的ID。 例如，在用户名字段中包含ID。
1. 步骤2中所述的操作将导致Primetime DRM向客户的服务器发送身份验证请求。 此请求包括设备证书：
   1. 服务器从请求和存储中提取设备证书和生成的ID。
   1. 客户子系统预生成此设备证书的许可证，存储这些许可证并以将它们与生成的ID关联的方式授予对它们的访问权。.
1. 服务器用“success”消息响应请求。
1. 应用程序存储生成的ID。

在设备注册后，应用程序使用生成的ID的方式与之前方案中使用设备ID的方式相同：
1. 应用程序将尝试查找生成的ID。
1. 如果找到生成的ID，则应用程序将在下载预生成的许可证时使用生成的ID。 应用程序将使用`DRMManager.storeVoucher()`方法将许可证发送到Primetime DRM客户端以供使用。.
1. 如果找不到生成的ID，则应用程序将完成设备注册过程。

## DRM工厂重置{#drm-factory-reset}

当设备用户调用DRM工厂重置选项时，将清除设备证书。 要继续播放受保护的内容，应用程序必须再次完成设备注册过程。 如果应用程序发送的预生成许可证已过期，则Primetime DRM客户端将拒绝该许可证，因为该许可证已针对旧设备ID进行加密。

* FlashAPI:[DRMManager.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers()) -（只能为响应某些不可恢复的DRM错误代码而调用。）
* iOS API:[DRMManager resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* Android API:[DRMManager.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))