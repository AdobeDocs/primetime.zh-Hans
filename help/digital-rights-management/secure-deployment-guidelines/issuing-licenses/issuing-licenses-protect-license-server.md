---
description: 您必须确保安全地颁发许可证。 请考虑这些最佳做法来保护许可证服务器
title: 保护许可证服务器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---

# 保护许可证服务器 {#protecting-the-license-server}

您必须确保安全地颁发许可证。 请考虑以下最佳实践来保护许可证服务器：

## 使用本地生成的CRL {#consuming-locally-generated-crls}

要使用本地生成的证书吊销列表(CRL)和策略更新列表，请使用Adobe Primetime DRM API验证签名。

以下API验证列表是否未被篡改，并且列表是由正确的许可证服务器签名的：

* 调用 [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) 以在提供 [吊销列表](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) 到任何API。

  有关更多信息，请参阅 [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* 调用 [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) 以在提供 `PolicyUpdateList` 到任何API。

  有关更多信息，请参阅 [策略更新列表](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## 使用Adobe发布的CRL{#consuming-crls-published-by-adobe}

SDK定期下载Adobe发布的CRL。 您必须确保不阻止对这些文件的访问，或者不阻止实施这些CRL。

SDK提供了一个配置选项，用于在检索AdobeCRL时忽略错误，并且您只能在开发环境中应用此选项。 在生产环境中，许可证服务器必须从Adobe中检索CRL。 如果许可证服务器无法获取有效的CRL，则出现错误。

## 生成CRL以补充Adobe发布的那些文档{#generating-crls-to-supplement-those-published-by-adobe}

您可以使用Adobe Primetime DRM创建CRL，以补充Adobe发布的计算机CRL。

Primetime DRM SDK检查并强制执行AdobeCRL。 但是，您可以通过创建一个CRL来禁止其他客户端计算机，该CRL可通过将CRL传递到Primetime DRM SDK来撤销其他计算机凭据。 当您颁发许可证时，SDK会检查AdobeCRL和您的CRL。

要生成CRL，请参阅 [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## 回滚检测 {#rollback-detection}

如果您的Adobe Primetime DRM实施使用要求客户端保持状态的业务规则（例如，播放窗口间隔），则Adobe建议服务器跟踪回滚计数器并使用AIR或SWF允许列表。

回滚计数器在来自客户端的大多数请求中发送到服务器。 如果您的Primetime DRM实施不需要回滚计数器，则可以忽略该计数器。 否则，Adobe建议服务器存储随机计算机ID，该ID是使用获取的 [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())以及数据库中的当前计数器值。

有关如何递增和跟踪回滚计数器的详细信息，请参见 [客户端状态](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) 和回滚检测。

## 颁发许可证时的计算机计数 {#machine-count-when-issuing-licenses}

如果业务规则要求跟踪用户的计算机数，则许可证服务器或域服务器必须存储与该用户关联的计算机ID。

跟踪计算机ID的最可靠方法是存储 [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) 数据库中的方法。 在收到新请求时，使用将请求中的计算机ID与已知的计算机ID进行比较 [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) 执行ID比较，以确定ID是否代表同一台计算机。 仅当机器ID数量较少时，这种比较才具有实用性。 例如，如果用户在其域中允许使用五台计算机，则可以在数据库中搜索与用户用户名关联的计算机ID，并获取一小部分数据以进行比较。

这种比较对于允许匿名访问的部署不实用。 在本例中， [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) 可以使用。 但是，如果用户从Flash和Adobe AIR®运行时访问内容，则此ID不能相同。

>[!NOTE]
>
>如果用户重新格式化硬盘，则ID将无法存留。

## 重播保护 {#replay-protection}

重播保护可防止攻击者重播许可证请求消息并可能导致对客户端的拒绝服务(DoS)攻击。

DoS攻击是攻击者试图阻止服务的合法用户使用该服务的一种尝试。 例如，使用回退计数器的重放攻击可能用来“欺骗”许可证服务器，使其认为DRM客户端已回退其状态，从而导致帐户暂停。

要了解有关重播保护的更多信息，请参阅 [AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).

## 维护受信任内容打包程序的允许列表 {#maintain-a-allowlist-of-trusted-content-packagers}

允许列表是受信任实体的列表。

对于内容打包者，实体是内容所有者信任的、用于打包（或加密）视频文件并创建受DRM保护的内容的组织。 在部署Adobe Primetime DRM时，您应该维护一个受信任的内容打包程序的允许列表。 在颁发许可证之前，您还必须验证受DRM保护文件的DRM元数据中的内容打包程序的身份。

要了解如何获取有关打包内容的实体的信息，请参阅 [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).

## 身份验证令牌超时{#timeout-for-authentication-tokens}

Adobe Primetime DRM SDK生成的所有身份验证令牌都有一个保护应用程序安全的超时间隔。

在处理身份验证请求时，使用Primetime DRM SDK指定身份验证令牌的过期时间。 令牌过期后不再有效，用户必须再次通过许可证服务器的身份验证。

要了解有关身份验证请求的更多信息，请参阅 [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## 覆盖策略选项 {#overriding-policy-options}

当您颁发许可证时，许可证服务器可以覆盖策略中指定的使用规则。

如果策略指定了开始日期，则不会在该开始日期之前生成许可证。 但是，您可以在生成许可证后，在许可证中设置未来的开始日期。 应谨慎使用此选项，因为客户端无法阻止用户向前移动系统时间以规避开始日期。
