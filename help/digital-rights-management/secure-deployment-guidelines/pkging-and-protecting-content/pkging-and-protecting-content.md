---
description: 有关打包和保护内容的信息使您能够保护内容。
title: 包装和保护内容
exl-id: f33d382b-07d7-4630-9e44-820d6249fee4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# 包装和保护内容 {#packaging-protecting-content}

有关打包和保护内容的信息使您能够保护内容。

## 保护服务器 {#securing-the-server}

您需要对进行策略管理和内容打包的计算机进行物理保护。

有关更多信息，请参阅 [物理安全和访问](../../secure-deployment-guidelines/physical-sec-and-access.md).

如果您的内容打包实施需要网络连接，则必须加固操作系统并实施适当的防火墙解决方案。 有关更多信息，请参阅 [网络拓扑](../../secure-deployment-guidelines/overview/network-topology.md).

## 安全地打包内容 {#securely-packaging-content}

Adobe Primetime DRM Media Packager命令行工具的配置文件要求在打包期间使用PKCS12凭据。

在“参考实施”命令行工具中，PKCS12凭据文件的密码存储在 `flashaccess.properties` 纯文本格式的文件。 因此，在保护承载此文件的计算机并确保计算机处于安全环境中时，请格外小心。 有关更多信息，请参阅 [物理安全和访问](../../secure-deployment-guidelines/physical-sec-and-access.md).

Packager还使用License Server和License Server传输证书，必须保护此信息的完整性和机密性。 应仅允许授权实体使用打包程序。 如果您的私钥被盗用，请立即通知Adobe Systems Incorporated以便吊销证书。

>[!NOTE]
>
>利用API，可对多个内容使用相同的密钥。 为确保最高级别的安全性，您应该只对多位速率FMS内容使用此功能。 请勿对代表不同内容的多个文件使用相同的密钥。

在某些情况下，Primetime DRM打包API会发出警告。 查看这些警告，以确定文件是否已成功加密。 警告消息可能是以下内容之一：

* 策略已过期，无法对无法识别的标记或跟踪进行加密。
* 无法加密影片片段，这些片段中的引用可能无效。
* 无法对元数据加密。

如果使用属性不正确的策略打包内容，则需要更新策略。 更新的策略必须通过策略更新列表或其他投放机制提供给许可证服务器。 创建策略后，无法更改某些策略属性。 如果这些属性不正确，请将内容从分发站点中拉回，撤销策略以便将来不会授予任何许可证，然后再次加密内容。

当打包完成后，打包密钥被垃圾收集，并且不会被明确销毁。 因此，封装密钥会保留在内存中一段时间。 您必须防止对计算机进行未经授权的访问，并确保不会公开任何可能泄露此信息的文件，例如核心转储。

## 安全存储策略 {#securely-storing-policies}

Adobe Primetime DRM SDK允许您开发可用于内容打包和策略创建的应用程序。

创建这些应用程序时，您可以允许某些用户创建和修改策略，并将其他用户限制为仅将现有策略应用于内容。 您必须实施必要的访问控制，并为策略创建和策略应用创建具有不同权限的用户帐户。

在策略用于打包之前，不会对其进行签名或修改。 如果您担心打包工具用户可能会修改策略，请签署策略以确保无法修改策略。

有关使用SDK创建应用程序的更多信息，请参阅 [API Primetime API参考](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).

## 非对称密钥加密 {#asymmetric-key-encryption}

非对称密钥加密（也称为公钥加密）使用密钥对。 一个密钥用于加密，另一个密钥用于解密。

解密密钥，或 *`private key`*，是保密的；加密密钥，或 *`public key`*，可供有权加密内容的任何用户使用。 有权访问公钥的任何人都可以加密内容。 但是，只有有权访问私钥的用户才能解密内容。 无法从公钥重建私钥。

当您打包内容时，许可证服务器的公钥用于加密DRM元数据中的内容加密密钥(CEK)。 您必须确保只有许可证服务器有权访问许可证服务器的私钥。 如果其他人拥有密钥，则可以解密和查看内容。

>[!CAUTION]
>
>确保从可信来源获取包含公钥的License Server证书。 这样，您就可以确保它是许可证服务器的密钥，而不是流氓公钥。 如果攻击者用他们的公钥替换许可证服务器的密钥，他们可以解密您的内容。

有关如何打包内容的更多信息，请参阅 [使用Adobe Primetime DRM SDK保护内容](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf).
