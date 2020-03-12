---
seo-title: 生成许可证
title: 生成许可证
uuid: f91b0cc8-e0ed-4722-947b-22eb2bfba916
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 生成许可证{#generating-licenses}

如果要向用户发布叶许可证，SDK必须解密内容元数据中包含的CEK，并为请求许可证的计算机重新加密它。 要解密CEK，服务器必须提供解密密钥所需的信息。 调 `ContentInfo.setKeyRetrievalInfo()` 用并提供对 `AsymmetricKeyRetrieval` 象。 如果元数据包括多个策略，则服务器必须确定要使用和调用的策略 `LicenseRequestMessage.setSelectedPolicy()`。 然后拨 `LicenseRequestMessage.generateLicense()` 叫以生成许可证。 使用 `License` 返回的对象，您可以修改许可证的到期时间或权限。

如果对 `ExternalKeyRetrieval` 象中指定了对象，则许可证服 `ContentInfo` 务器应使用关联的CEK ID来检索插入到许可证中的相应CEK。

有关如何 [使用外部CEK工作流程的更多详细信息](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md) ，请参阅Adobe Primetime DRM外部CEK概述。
