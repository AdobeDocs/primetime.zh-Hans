---
title: 安全地打包内容
description: 安全地打包内容
copied-description: true
exl-id: f554852c-83d9-4b31-8dde-2af577c70989
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 安全地打包内容 {#securely-packaging-content}

AdobeAccess Media Packager命令行工具的配置文件要求在打包期间使用PKCS12凭据。

在参考实施命令行工具中，PKCS12凭据文件的密码以明文形式存储在flashaccess.properties文件中。 因此，在保护托管此文件的计算机时，请格外小心，并确保它处于安全的环境中。 (请参阅 [物理安全和访问](../../aaxs-secure-deployment-guidelines/physical-sec-and-access.md))。

Packager还使用License Server和License Server传输证书。 必须保护此信息的完整性和机密性。 应仅允许授权实体使用打包程序。 如果您的任何私钥被泄露，请立即通知Adobe Systems Incorporated以便可以吊销证书。

>[!NOTE]
>
>利用API，可对多个内容使用相同的密钥。 为确保最高级别的安全性，我们建议仅将此功能用于多比特率FMS内容。 对于表示不同内容的多个文件，建议不要使用相同的键。

在某些情况下，Adobe访问打包API会发出警告。 您必须查看这些警告，以确定文件是否已成功加密。 警告消息可能会声明策略已过期，不会加密无法识别的标记或跟踪，不会加密影片片段（并且这些片段内的引用可能无效），也不会加密元数据。

如果使用具有不正确属性的策略打包内容，则应该更新策略，并且更新的策略必须通过策略更新列表或用于将更新的策略传递到服务器的其他机制提供给许可证服务器。 创建策略后，无法更改某些策略属性。 如果这些属性不正确，请将内容从分发站点中拉回，撤销策略以便将来不会授予任何许可证，然后重新加密内容。

打包完成后，不会显式销毁打包密钥；但是，会进行垃圾收集。 因此，打包密钥会在一段时间内保留在内存中；您必须防止对计算机进行未经授权的访问，并采取措施确保不会公开任何可能泄露此信息的文件，如核心转储。
