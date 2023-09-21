---
title: 在Adobe颁发的证书过期时处理证书更新
description: 在Adobe颁发的证书过期时处理证书更新
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# 在Adobe颁发的证书过期时处理证书更新 {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

有时可能必须从Adobe中获取新证书。 例如，生产证书过期时、评估证书过期时，或者从评估证书切换到生产证书时。 证书过期时，您不希望重新打包使用旧证书的内容。 您可以使License Server知道旧证书和新证书。

使用以下过程使用新证书更新服务器：

1. （可选）将新条目添加到现有策略更新列表或吊销列表时，请确保使用新凭据进行签名，并使用旧证书验证现有文件上的签名。

   例如，使用以下命令行将条目添加到使用其他凭据签名的现有策略更新列表中：

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. 使用Java API使用新的策略更新列表或吊销列表更新许可证服务器：

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   或：

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   在参考实现中，您使用的属性包括 `HandlerConfiguration.RevocationList` 和 `HandlerConfiguration.PolicyUpdateList`. 同时更新用于验证签名的证书： `RevocationList.verifySignature.X509Certificate`.

1. 要使用使用旧证书打包的内容，许可证服务器需要旧和新的许可证服务器凭据以及传输凭据。 使用新证书和旧证书更新许可证服务器。

   对于许可证服务器凭据：

   * 确保将当前凭据传递到 `LicenseHandler` 构造函数：

      * 在参考实施中，通过 `LicenseHandler.ServerCredential` 属性。
      * 在Adobe Access Server for Protected Streaming中，当前凭据必须是中指定的第一个凭据 `LicenseServerCredential` flashaccess-tenant.xml文件中的元素。

   * 确保向提供当前凭证和旧凭证 `AsymmetricKeyRetrieval`

      * 在参考实施中，通过 `LicenseHandler.ServerCredential` 和 `AsymmetricKeyRetrieval.ServerCredential. n` 属性。
      * 在Adobe Access Server for Protected Streaming中，旧凭据在 `LicenseServerCredential` flashaccess-tenant.xml文件中的元素。

   对于传输凭据：

   * 确保将当前凭据传递到 `HandlerConfiguration.setServerTransportCredential()` 方法：

      * 在参考实施中，通过 `HandlerConfiguration.ServerTransportCredential` 属性。
      * 在Adobe Access Server中，对于受保护的流式传输，当前凭据必须是中指定的第一个凭据。 `TransportCredential` flashaccess-tenant.xml文件中的元素。

   * 确保向提供旧凭据 `HandlerConfiguration.setAdditionalServerTransportCredentials`()：

      * 在参考实施中，通过 `HandlerConfiguration.AdditionalServerTransportCredential. n` 属性。
      * 在用于受保护流的Adobe Access Server中，此参数在 `TransportCredential` flashaccess-tenant.xml文件中的元素。

1. 更新打包工具，确保它们使用当前凭据打包内容。 请确保使用最新的许可证服务器证书、传输证书和打包程序凭据进行打包。
1. 要更新密钥服务器的许可证服务器证书，请执行以下操作：

   * 更新Adobe访问密钥服务器租户配置文件中的凭据。 在flashaccess-keyserver-tenant.xml中包含旧密钥服务器凭据和新密钥服务器凭据。
   * 确保将当前证书传递到 `HandlerConfiguration.setKeyServerCertificate()` 方法。

      * 在参考实施中，通过 `HandlerConfiguration.KeyServerCertificate` 属性。
      * 在适用于受保护流的Adobe Access Server中，通过Configuration/Tenant/Certificates/KeyServer元素在中指定密钥服务器的证书。
