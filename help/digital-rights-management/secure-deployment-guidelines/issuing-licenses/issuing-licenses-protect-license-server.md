---
description: '您必须确保安全地颁发许可证。 考虑这些保护许可证服务器的最佳实践 '
seo-description: '您必须确保安全地颁发许可证。 考虑这些保护许可证服务器的最佳实践 '
seo-title: 保护许可证服务器
title: 保护许可证服务器
uuid: 7b5de17d-d0a7-41df-9651-4ff51c9965c6
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 保护许可证服务器 {#protecting-the-license-server}

您必须确保安全地颁发许可证。 请考虑以下最佳实践以保护许可证服务器：

## 使用本地生成的CRL {#consuming-locally-generated-crls}

要使用本地生成的证书撤销列表(CRL)和策略更新列表，请使用Adobe Primetime DRM API验证签名。

以下API验证列表是否未被篡改，以及列表是否已由正确的许可证服务器签名：

* 调用 [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) ，以在向任何API提供 [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) 之前检查签名。

   有关详细信息，请参 [阅RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。

* 调用 [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) ，以在向任何API提供签名之 `PolicyUpdateList` 前检查签名。

   有关详细信息，请参 [阅PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html)。

## 使用Adobe发布的CRL{#consuming-crls-published-by-adobe}

SDK会定期下载Adobe发布的CRL。 您必须确保不会阻止对这些文件的访问，或者不会阻止执行这些CRL。

SDK具有一个配置选项，可在检索Adobe CRL时忽略错误，并且您只能在开发环境中应用此选项。 在生产环境中，许可证服务器必须从Adobe检索CRL。 如果许可证服务器无法获得有效的CRL，则发生错误。

## 生成CRL以补充Adobe发布的CRL{#generating-crls-to-supplement-those-published-by-adobe}

您可以使用Adobe Primetime DRM创建CRL，这些CRL是Adobe发布的计算机CRL的补充。

Primetime DRM SDK检查并执行Adobe CRL。 但是，您可以通过创建CRL来禁止其他客户端计算机，该CRL通过将CRL传递到Primetime DRM SDK来撤销其他计算机凭据。 在您发出许可证时，SDK会检查Adobe CRL和您的CRL。

要生成CRL，请参 [阅RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。

## 回滚检测 {#rollback-detection}

如果您实施Adobe Primetime DRM时使用要求客户端保持状态（例如，播放窗口间隔）的业务规则，Adobe建议服务器跟踪回滚计数器并使用AIR或SWF白名单。

回滚计数器在来自客户端的大多数请求中发送到服务器。 如果您实施Primetime DRM时不需要回滚计数器，则可以忽略它。 否则，Adobe建议服务器存储随机计算机ID(使用 [MachineToken.getUniqueId()获取)](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())，以及数据库中的当前计数器值。

有关如何增加和跟踪回滚计数器的详细信息，请参 [阅ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) 和Rollback detection。

## 颁发许可证时的计算机计数 {#machine-count-when-issuing-licenses}

如果业务规则要求跟踪用户的计算机数，则许可证服务器或域服务器必须存储与用户关联的计算机ID。

跟踪机器ID的最可靠方法是将 [MachineId.getBytes()方法返回的值存储在数据库中](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) 。 收到新请求后，请使用 [MachineId.matches()将请求中的计算机ID与已知的计算机ID进行比较](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId))。

[MachineId.matches()执行ID比较](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) ，以确定ID是否代表同一台计算机。 此比较仅在机器ID数量较少时才可用。 例如，如果用户在其域中被允许使用五台计算机，则可以在数据库中搜索与用户用户名关联的计算机ID，并获取一小组数据进行比较。

此比较对于允许匿名访问的部署来说不现实。 在这种情况下， [可以使用MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) 。 但是，如果用户从Flash和Adobe AIR®运行时访问内容，则此ID不能相同。

>[!NOTE]
>
>如果用户重新设置硬盘的格式，则ID将不再有效。

## 重放保护 {#replay-protection}

重放保护可防止攻击者重放许可证请求消息并可能对客户端造成拒绝服务(DoS)攻击。

DoS攻击是攻击者试图阻止某个服务的合法用户使用该服务。 例如，使用回滚计数器的重放攻击可用于“欺骗”许可证服务器，使其认为DRM客户端已回滚其状态，这会导致帐户挂起。

要了解有关重放保护的更多信息，请 [ 参阅AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId())。

## 维护受信任的内容包装程序的白名单{#maintain-a-whitelist-of-trusted-content-packagers}

白名单是受信任实体的列表。

对于内容打包程序，实体是内容所有者信任的组织，可以打包（或加密）视频文件并创建DRM保护的内容。 部署Adobe Primetime DRM时，您应当保留受信任内容打包程序的白名单。 在发布许可证之前，还必须验证受DRM保护的文件的DRM元数据中的内容打包程序的标识。

要了解如何获取有关打包内容的实体的信息，请参 [阅V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo())。

## 身份验证令牌超时{#timeout-for-authentication-tokens}

由Adobe Primetime DRM SDK生成的所有身份验证令牌都有一个超时间隔，以保护应用程序安全。

在处理身份验证请求时，使用Primetime DRM SDK指定身份验证令牌的到期时间。 在令牌过期后，该令牌不再有效，用户必须再次与许可证服务器进行身份验证。

要了解有关身份验证请求的更多信息，请参 [阅AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html)。

## 覆盖策略选项 {#overriding-policy-options}

在您发布许可证时，许可证服务器可以覆盖策略中指定的使用规则。

如果策略指定了开始日期，则不会在该开始日期之前生成许可证。 但是，您可以在生成许可证后在许可证中设置将来的开始日期。 应谨慎使用此选项，因为客户端无法阻止用户将系统时间向前移动以规避开始日期。