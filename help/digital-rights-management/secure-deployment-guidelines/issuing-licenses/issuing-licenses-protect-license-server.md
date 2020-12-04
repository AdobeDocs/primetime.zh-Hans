---
description: '您必须确保安全地颁发许可证。 考虑这些保护许可证服务器的最佳实践 '
seo-description: '您必须确保安全地颁发许可证。 考虑这些保护许可证服务器的最佳实践 '
seo-title: 保护许可证服务器
title: 保护许可证服务器
uuid: 7b5de17d-d0a7-41df-9651-4ff51c9965c6
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---


# 保护许可证服务器{#protecting-the-license-server}

您必须确保安全地颁发许可证。 请考虑以下保护许可证服务器的最佳实践：

## 正在使用本地生成的CRL {#consuming-locally-generated-crls}

要使用本地生成的证书吊销列表(CRL)和策略更新列表，请使用Adobe PrimetimeDRM API验证签名。

以下API验证列表未被篡改，且列表已由正确的许可证服务器进行签名：

* 调用[RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate))检查签名，然后将[ RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html)提供给任何API。

   有关详细信息，请参阅[RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。

* 调用[PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate))检查签名，然后将`PolicyUpdateList`提供给任何API。

   有关详细信息，请参阅[PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html)。

## 使用Adobe{#consuming-crls-published-by-adobe}发布的CRL

SDK会定期下载由Adobe发布的CRL。 必须确保不阻止访问这些文件，或不阻止执行这些CRL。

SDK具有一个配置选项，用于在检索AdobeCRL时忽略错误，并且您只能在开发环境中应用此选项。 在生产环境中，许可证服务器必须从Adobe检索CRL。 如果许可证服务器无法获取有效的CRL，则出现错误。

## 生成CRL以补充由Adobe{#generating-crls-to-supplement-those-published-by-adobe}发布的CRL

您可以使用Adobe PrimetimeDRM创建补充由Adobe发布的计算机CRL的CRL。

Primetime DRM SDK检查并执行AdobeCRL。 但是，您可以通过创建CRL来禁止其他客户端计算机，该CRL通过将CRL传递到Primetime DRM SDK来撤消其他计算机凭据。 发出许可证时，SDK将检查AdobeCRL和您的CRL。

要生成CRL，请参阅[RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。

## 回滚检测{#rollback-detection}

如果您的Adobe PrimetimeDRM实施使用要求客户端保持状态（例如，播放窗口间隔）的业务规则，则Adobe建议服务器跟踪回滚计数器，并使用AIR或SWF允许列表。

回滚计数器在客户端发出的大多数请求中都发送到服务器。 如果您的Primetime DRM实施不需要回滚计数器，则可忽略它。 否则，Adobe建议服务器存储随机计算机ID(使用[MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())获取)以及数据库中的当前计数器值。

有关如何增加和跟踪回滚计数器的详细信息，请参阅[ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html)和回滚检测。

## 颁发许可证{#machine-count-when-issuing-licenses}时的计算机计数

如果业务规则要求跟踪用户的计算机数，则许可证服务器或域服务器必须存储与用户关联的计算机ID。

跟踪机器ID的最可靠方法是将[MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes())方法返回的值存储在数据库中。 收到新请求时，请使用[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId))将请求中的计算机ID与已知的计算机ID进行比较。

[MachineId.matches()执](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) 行ID的比较，以确定ID是否代表同一台计算机。此比较仅在机器ID数较少时才可用。 例如，如果允许用户在其域中使用五台计算机，则可以搜索数据库以找到与用户用户名关联的计算机ID，并获取一小组数据进行比较。

此比较对于允许匿名访问的部署来说不实用。 在这种情况下，可以使用[MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())。 但是，如果用户从Flash和Adobe AIR®运行时访问内容，则此ID不能相同。

>[!NOTE]
>
>如果用户重新格式化硬盘，则ID将不会存在。

## 重放保护{#replay-protection}

重放保护可防止攻击者重放许可证请求消息并可能对客户端造成拒绝服务(DoS)攻击。

DoS攻击是攻击者试图阻止服务的合法用户使用该服务。 例如，使用回滚计数器的重放攻击可用于“诱骗”许可证服务器，使其认为DRM客户端已回滚其状态，这会导致帐户挂起。

要了解有关重放保护的更多信息，请参阅[ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId())。

## 维护受信任内容包装程序的允许列表{#maintain-a-allowlist-of-trusted-content-packagers}

允许列表是受信任实体的列表。

对于内容打包者，实体是内容所有者信任的组织，可以打包（或加密）视频文件并创建DRM保护的内容。 部署Adobe PrimetimeDRM时，您应当维护一允许列表可信的内容打包程序。 在颁发许可证之前，还必须验证受DRM保护的文件的DRM元数据中的内容打包程序的身份。

要了解如何获取有关打包内容的实体的信息，请参阅[V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo())。

## 身份验证令牌超时{#timeout-for-authentication-tokens}

由Adobe PrimetimeDRM SDK生成的所有身份验证令牌都有一个超时时间间隔，以保护应用程序安全。

在处理身份验证请求时，使用Primetime DRM SDK指定身份验证令牌的过期时间。 该令牌过期后，该令牌不再有效，用户必须再次与许可证服务器进行身份验证。

要了解有关身份验证请求的更多信息，请参阅[AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html)。

## 正在覆盖策略选项{#overriding-policy-options}

发出许可证时，许可证服务器可以覆盖策略中指定的使用规则。

如果策略指定了开始日期，则不会在该开始日期之前生成许可证。 但是，您可以在许可证生成后在许可证中设置未来开始日期。 此选项应谨慎使用，因为客户端无法阻止用户将系统时间向前移动以避开开始日期。