---
seo-title: 在Adobe颁发的证书过期时处理证书更新
title: 在Adobe颁发的证书过期时处理证书更新
uuid: abc0ca3e-a78f-4078-9480-7116843cce05
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 在Adobe颁发的证书过期时处理证书更新{#handling-certificate-updates-when-adobe-issued-certificates-expire}

您可能需要从Adobe获得新证书。 例如，当评估证书过期或从评估证书切换到生产证书时，生产证书将过期。 只要证书过期且您不希望重新打包使用旧证书的内容，您就可以使许可证服务器同时了解旧证书和新证书。

使用新证书更新服务器：

1. （可选）当您向现有DRM策略更新列表或撤销列表添加新条目时，您需要使用新凭据进行签名，并使用旧证书验证现有文件上的签名。

   例如，您可以使用以下命令行向现有DRM策略更新列表添加一个条目，该列表已使用其他凭据进行签名：

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. （可选）使用Java API使用新的DRM策略更新列表或撤销列表更新许可证服务器：

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   或：

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   在引用实现中，您使用的属性是 `HandlerConfiguration.RevocationList` 和 `HandlerConfiguration.PolicyUpdateList`。 您还需要更新用于验证签名的证书： `RevocationList.verifySignature.X509Certificate`.

1. 使用新证书和旧证书更新许可证服务器。

   如果要使用使用旧证书打包的内容，请确保许可证服务器有权访问旧的和新的许可证服务器凭据以及传输凭据。

   对于许可证服务器凭据：

   * 确保将当前凭据传递给构造函 `LicenseHandler` 数：

      * 在引用实现中，使用属性设置 `LicenseHandler.ServerCredential` 它。
      * 在Adobe Primetime DRM Server的受保护流中，当前凭证必须是flashaccess-tenant.xml文件中元素中指定的 `LicenseServerCredential` 第一个凭证。
   * 确保向 `AsymmetricKeyRetrieval`

      * 在引用实现中，使用和属性设置 `LicenseHandler.ServerCredential` 它 `AsymmetricKeyRetrieval.ServerCredential. n` 。

      * 在Primetime DRM Server中，旧凭据在flashaccess-tenant.xml文件中元素中的第一个凭据之后指定 `LicenseServerCredential` ，用于保护流。
   对于传输凭据：

   * 确保将当前凭据传递给方 `HandlerConfiguration.setServerTransportCredential()` 法：

      * 在引用实现中，使用属性设置 `HandlerConfiguration.ServerTransportCredential` 它。
      * 在Primetime DRM Server中，对于受保护的流，当前凭证必须是文件中元素中指定的 `TransportCredential` 第一个凭 [!DNL flashaccess-tenant.xml] 据。
   * 确保向()提供旧凭 `HandlerConfiguration.setAdditionalServerTransportCredentials`据：

      * 在引用实现中，使用属性设置 `HandlerConfiguration.AdditionalServerTransportCredential. n` 它。
      * 在Primetime DRM Server中，对于受保护的流，在flashaccess-tenant.xml文件中的元素中的第 `TransportCredential` 一个凭据后指定此凭据。




1. 更新打包工具，确保它们使用当前凭据打包内容。 确保使用最新的许可证服务器证书、传输证书和包装程序凭据进行打包。
1. 按如下方式更新密钥服务器的许可证服务器证书：

   * 通过在flashaccess-keyserver-tenant.xml中同时包含旧的和新的Key Server凭据，更新Adobe Primetime DRM Key Server租户配置文件中的凭据。
   * 确保将当前证书传递给该方 `HandlerConfiguration.setKeyServerCertificate()` 法。

      * 在引用实现中，使用属性设置 `HandlerConfiguration.KeyServerCertificate` 它。
      * 在Primetime DRM Server的受保护流中，通过Configuration/Tenant/Certificates/KeyServer元素指定Key Server的证书。

