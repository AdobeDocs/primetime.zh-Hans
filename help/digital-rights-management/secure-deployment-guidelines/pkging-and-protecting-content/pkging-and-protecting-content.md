---
description: 有关内容打包和保护的信息允许您保护内容。
seo-description: 有关内容打包和保护的信息允许您保护内容。
seo-title: 包装和保护内容
title: 包装和保护内容
uuid: 9bf89f86-082e-40f9-8deb-c9774a9d8e02
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---


# 打包和保护内容{#packaging-protecting-content}

有关内容打包和保护的信息允许您保护内容。

## 保护服务器{#securing-the-server}

您需要物理地保护发生策略管理和内容打包的计算机。

有关详细信息，请参阅[物理安全和访问](../../secure-deployment-guidelines/physical-sec-and-access.md)。

如果内容打包实施需要网络连接，则必须强化操作系统并实施适当的防火墙解决方案。 有关详细信息，请参阅[网络拓扑](../../secure-deployment-guidelines/overview/network-topology.md)。

## 安全地打包内容{#securely-packaging-content}

Adobe PrimetimeDRM Media Packager命令行工具的配置文件需要在打包过程中使用的PKCS12凭据。

在“Reference Implementation（参考实施）”命令行工具中，PKCS12凭据文件的口令以明文形式存储在`flashaccess.properties`文件中。 因此，在保护承载此文件的计算机并确保计算机处于安全环境时，请格外小心。 有关详细信息，请参阅[物理安全和访问](../../secure-deployment-guidelines/physical-sec-and-access.md)。

该包装程序还使用许可证服务器和许可证服务器传输证书，并且必须保护这些信息的完整性和机密性。 仅允许授权实体使用包装程序。 如果您的私钥被泄露，请立即通知Adobe Systems Incorporated，以便吊销证书。

>[!NOTE]
>
>API允许您对多个内容使用相同的密钥。 要确保最高级别的安全性，您应仅对多比特率FMS内容使用此功能。 请勿对表示不同内容的多个文件使用相同的键。

Primetime DRM打包API在某些条件下发出警告。 查看这些警告以确定您的文件是否已成功加密。 警告消息可能是以下消息之一：

* 策略已过期，无法加密无法识别的标记或跟踪。
* 无法加密电影片段，这些片段中的引用可能无效。
* 元数据无法加密。

如果内容是通过使用属性不正确的策略进行打包的，则需要更新策略。 更新的策略必须通过策略更新列表或其他投放机制提供给许可证服务器。 创建策略后，无法更改某些策略属性。 如果这些属性不正确，请从分发站点中拉回内容，撤销策略以便将来不能授予许可证，然后重新加密内容。

打包完成后，打包密钥将被垃圾回收，并且不会被显式销毁。 因此，封装密钥在内存中保留一段时间。 您必须防止对计算机进行未经授权的访问，并确保不泄露任何可能泄露此信息的文件，如核心转储。

## 安全地存储策略{#securely-storing-policies}

Adobe PrimetimeDRM SDK允许您开发可用于内容打包和策略创建的应用程序。

在创建这些应用程序时，您可以允许一些用户创建和修改策略，并限制其他用户仅将现有策略应用于内容。 必须实施必要的访问控制，并创建具有不同权限的用户帐户，以便进行策略创建和策略应用。

在打包中使用策略之前，策略不会进行签名或不会进行修改。 如果您担心打包工具用户可能修改策略，请签署策略以确保无法修改策略。

有关使用SDK创建应用程序的详细信息，请参阅[API Primetime API References](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References)上的Primetime DRM API。

## 非对称密钥加密{#asymmetric-key-encryption}

非对称密钥加密也称为公钥加密，它使用对密钥。 一个密钥用于加密，另一个密钥用于解密。

解密密钥或&#x200B;*`private key`*&#x200B;是保密的；加密密钥或&#x200B;*`public key`*&#x200B;对任何有权加密内容的人都可用。 有权访问公钥的任何人都可以加密内容。 但是，只有有权访问私钥的人才能解密内容。 无法从公钥重建私钥。

打包内容时，许可证服务器的公钥用于加密DRM元数据中的内容加密密钥(CEK)。 您必须确保只有许可证服务器才有权访问许可证服务器的私钥。 如果有人有密钥，他们可以解密和视图内容。

>[!CAUTION]
>
>确保从受信任源获得包含公钥的许可证服务器的证书。 这样，您就可以确保它是许可证服务器的密钥，而不是流氓公钥。 如果攻击者用其公钥替换许可证服务器的密钥，他们可以解密您的内容。

有关如何打包内容的详细信息，请参阅[使用Adobe PrimetimeDRM SDK for Protecting Content](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf)。