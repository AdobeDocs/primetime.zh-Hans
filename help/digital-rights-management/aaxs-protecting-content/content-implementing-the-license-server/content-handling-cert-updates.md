---
seo-title: 在Adobe颁发的证书过期时处理证书更新
title: 在Adobe颁发的证书过期时处理证书更新
uuid: 5151ef15-daf6-4fb3-bf83-25ebac1d003b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 在Adobe颁发的证书过期时处理证书更新 {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

有时您可能必须从Adobe获得新证书。 例如，当生产证书过期时，评估证书过期，或者从评估证书切换到生产证书时。 当证书过期且您不希望重新打包使用旧证书的内容时。 您可以使许可证服务器了解新旧证书。

请按照以下过程使用新证书更新服务器：

1. （可选）向现有策略更新列表或撤销列表添加新条目时，请务必使用新凭据进行签名，然后使用旧证书验证现有文件上的签名。

   例如，使用以下命令行向现有策略更新列表添加一个条目，该列表使用其他凭据进行签名：

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. 使用Java API使用新策略更新列表或撤销列表更新许可证服务器：

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   或：

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   在引用实现中，您使用的属性是 `HandlerConfiguration.RevocationList` 和 `HandlerConfiguration.PolicyUpdateList`。 同时更新用于验证签名的证书： `RevocationList.verifySignature.X509Certificate`.

1. 要使用使用旧证书打包的内容，许可证服务器需要新旧许可证服务器凭据和传输凭据。 使用新证书和旧证书更新许可证服务器。

   对于许可证服务器凭据：

   * 确保将当前凭据传递给构造 `LicenseHandler` 函数：

      * 在引用实现中，通过属性设置 `LicenseHandler.ServerCredential` 它。
      * 在Adobe Access Server的受保护流中，当前凭据必须是flashaccess-tenant.xml文件中元素中指 `LicenseServerCredential` 定的第一个凭据。
   * 确保向 `AsymmetricKeyRetrieval`

      * 在引用实现中，通过和属性设置 `LicenseHandler.ServerCredential` 它 `AsymmetricKeyRetrieval.ServerCredential. n` 。
      * 在Adobe Access Server的受保护流中，旧凭据在flashaccess-tenant.xml文件中元素中的第一个凭据 `LicenseServerCredential` 之后指定。
   对于传输凭据：

   * 确保将当前凭据传递给以下方 `HandlerConfiguration.setServerTransportCredential()` 法：

      * 在引用实现中，通过属性设置 `HandlerConfiguration.ServerTransportCredential` 它。
      * 在Adobe Access Server中，当前凭据必须是flashaccess-tenant.xml文件中元素中指 `TransportCredential` 定的第一个凭据。
   * 确保向()提供旧凭 `HandlerConfiguration.setAdditionalServerTransportCredentials`据：

      * 在引用实现中，通过属性设置 `HandlerConfiguration.AdditionalServerTransportCredential. n` 它。
      * 在Adobe Access Server中，对于受保护的流，在flashaccess-tenant.xml文件中元素中的第 `TransportCredential` 一个凭据后指定此凭据。




1. 更新打包工具，确保它们使用当前凭据打包内容。 确保使用最新的许可证服务器证书、传输证书和包装程序凭据进行打包。
1. 更新密钥服务器的许可证服务器证书：

   * 更新Adobe Access Key Server租户配置文件中的凭据。 在flashaccess-keyserver-tenant.xml中包含旧的和新的密钥服务器凭据。
   * 确保将当前证书传递到该方 `HandlerConfiguration.setKeyServerCertificate()` 法。

      * 在引用实现中，通过属性设置 `HandlerConfiguration.KeyServerCertificate` 它。
      * 在Adobe Access Server的受保护流中，通过Configuration/Tenant/Certificates/KeyServer元素在中指定Key Server的证书。

