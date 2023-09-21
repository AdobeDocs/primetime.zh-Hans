---
title: 许可证预览
description: 许可证预览
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# 许可证预览 {#license-preview}

如果对设备是否可以使用和完全强制执行Primetime DRM许可证存在疑问，则可以使用许可证预览功能。 预览许可证与最终许可证中定义的所有限制和限制完全匹配，但不包含解密受保护内容所需的内容加密密钥(CEK)。 此功能可用于在内容分发器决定向客户端提供特定许可证之前，确定客户端是否确实可以使用许可证。 例如，客户希望观看高清内容，但内容分发商希望确保设备能够完全检测和参与HDCP。 在这种情况下，客户端可以调用 `DRMManager.loadPreviewVoucher()`. 如果 `DRMStatusEvent` 接收的是，而不是 `DRMErrorEvent`然后确认客户端可以完全执行许可证中的输出保护限制，并且内容分发器可以自由地向客户端提供此类许可证。

[iOS acquirePreviewLicense：](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquirePreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
