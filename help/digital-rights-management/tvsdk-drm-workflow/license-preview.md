---
seo-title: 许可预览
title: 许可预览
uuid: 61ff171f-b977-40ef-8e8d-2900316fa89a
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# 许可预览{#license-preview}

如果设备是否可以使用并完全执行Primetime DRM许可证存在问题，则可以使用许可证预览功能。 预览许可证完全匹配最终许可证中定义的所有约束和限制，但不包含解密受保护内容所需的内容加密密钥(CEK)。 此功能有助于在内容分销商决定向客户提供特定许可之前确定客户是否确实可以使用该许可。 例如，客户希望观看高清内容，但内容分销商希望确保设备能够完全检测并吸引HDCP。 在这种情况下，客户端可以调用`DRMManager.loadPreviewVoucher()`。 如果收到`DRMStatusEvent`，而不是`DRMErrorEvent`，则确认客户端可以在许可证中完全执行输出保护限制，内容分发商可以向客户端自由提供此类许可证。

[iOS acquirePreviewLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquirePreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
