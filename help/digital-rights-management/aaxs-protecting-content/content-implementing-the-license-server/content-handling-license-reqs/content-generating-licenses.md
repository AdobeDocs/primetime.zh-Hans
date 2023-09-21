---
title: 正在生成许可证
description: 正在生成许可证
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# 正在生成许可证 {#generating-licenses}

要向用户颁发叶许可证，SDK必须解密内容元数据中包含的CEK，并为请求许可证的计算机重新加密它。 要解密CEK，服务器必须提供解密密钥所需的信息。 调用 `ContentInfo.setKeyRetrievalInfo()` 并提供 `AsymmetricKeyRetrieval` 对象。 如果元数据包含多个策略，则服务器必须确定要使用的策略并调用 `LicenseRequestMessage.setSelectedPolicy()`. 然后调用 `LicenseRequestMessage.generateLicense()` 以生成许可证。 使用 `License` 返回的对象，您可以修改许可证中的到期或权限。

如果指定了ExternalKeyRetrieval对象 `ContentInfo` 对象，则许可证服务器应使用关联的CEK ID来获取将插入到许可证中的适当CEK。 有关如何使用外部CEK工作流的更多详细信息，请参阅 [Adobe访问DRM外部CEK概述](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)
