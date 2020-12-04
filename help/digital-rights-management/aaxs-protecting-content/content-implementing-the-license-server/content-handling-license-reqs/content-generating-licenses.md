---
seo-title: 生成许可证
title: 生成许可证
uuid: 242d5567-f609-4781-a8a6-2f3d78471344
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# 生成许可证{#generating-licenses}

要向用户发布叶许可证，SDK必须解密内容元数据中包含的CEK，并为请求许可证的计算机重新加密它。 要解密CEK，服务器必须提供解密密钥所需的信息。 调用`ContentInfo.setKeyRetrievalInfo()`并提供`AsymmetricKeyRetrieval`对象。 如果元数据包含多个策略，则服务器必须确定要使用的策略并调用`LicenseRequestMessage.setSelectedPolicy()`。 然后调用`LicenseRequestMessage.generateLicense()`生成许可证。 使用返回的`License`对象，您可以修改许可证的过期时间或权限。

如果在`ContentInfo`对象中指定了ExternalKeyRetrieval对象，则许可证服务器应使用关联的CEK ID来获取将插入到许可证中的相应CEK。 有关如何使用外部CEK工作流的详细信息，请参阅[Adobe访问DRM外部CEK概述](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)
