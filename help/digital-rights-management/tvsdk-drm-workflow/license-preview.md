---
title: 许可预览
description: 许可预览
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# 许可证预览{#license-preview}

如果有关设备是否可以使用和完全实施Primetime DRM许可证的问题，您可以使用许可证预览功能。 预览许可证完全匹配最终许可证中定义的所有约束和限制，但不包含解密受保护内容所需的内容加密密钥(CEK)。 此功能有助于确定客户在内容分销商决定向客户提供特定许可证之前是否确实可以使用许可证。 例如 — 客户希望观看高清内容，但内容分销商希望确保设备能够完全检测并使用HDCP。 在这种情况下，客户端可以调用`DRMManager.loadPreviewVoucher()`。 如果收到`DRMStatusEvent`，而不是`DRMErrorEvent`，则确认客户端可以完全执行许可证中的输出保护限制，内容分发商可以免费向客户端提供此类许可证。

[iOS acquirePreviewLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquirePreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
