---
seo-title: 许可证预览
title: 许可证预览
uuid: 61ff171f-b977-40ef-8e8d-2900316fa89a
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 许可证预览 {#license-preview}

如果设备是否可以使用并完全强制使用Primetime DRM许可证存在问题，则可以使用许可证预览功能。 预览许可证完全匹配最终许可证中定义的所有约束和限制，但不包含解密受保护内容所需的内容加密密钥(CEK)。 此功能有助于确定客户在内容分销商决定向客户提供特定许可之前是否确实可以使用该许可。 例如，客户希望观看高清内容，但内容分销商希望确保设备能够完全检测并使用HDCP。 在这种情况下，客户可以呼叫 `DRMManager.loadPreviewVoucher()`。 如果收 `DRMStatusEvent` 到的不是输出保护 `DRMErrorEvent`，则确认客户端可以在许可中完全执行输出保护限制，内容发行商可以向客户端自由提供此类许可。

[iOS获取PreviewLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquirePreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
