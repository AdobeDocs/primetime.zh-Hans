---
title: 处理Adobe颁发的证书过期时的证书更新
description: 处理Adobe颁发的证书过期时的证书更新
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# 处理Adobe颁发的证书过期时的证书更新{#handling-certificate-updates-when-adobe-issued-certificates-expire}

您可能需要从Adobe获取新的证书。 例如，生产证书将在评估证书过期时过期，或者当您从评估证书切换到生产证书时过期。 当证书过期并且您不想重新打包使用旧证书的内容时，您可以使许可证服务器知道旧证书和新证书。

要使用新证书更新服务器，请执行以下操作：

1. （可选）将新条目添加到现有DRM策略更新列表或吊销列表时，需要使用新凭据进行签名，并使用旧证书验证现有文件上的签名。

   例如，可以使用以下命令行将条目添加到已使用其他凭据签名的现有DRM策略更新列表中：

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. （可选）使用Java API使用新的DRM策略更新列表或吊销列表更新许可证服务器：

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   或：

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   在参考实施中，您使用的属性为 `HandlerConfiguration.RevocationList` 和 `HandlerConfiguration.PolicyUpdateList`. 您还需要更新用于验证签名的证书： `RevocationList.verifySignature.X509Certificate`.

1. 使用新证书和旧证书更新许可证服务器。

   如果要使用使用使用旧证书打包的内容，请确保许可证服务器可以访问旧和新的许可证服务器凭据以及传输凭据。

   对于许可证服务器凭据：

   * 确保将当前凭据传递到 `LicenseHandler` 构造函数：

      * 在参考实施中，使用 `LicenseHandler.ServerCredential` 属性。
      * 在Adobe Primetime DRM Server for Protected Streaming中，当前凭据必须是中指定的第一个凭据。 `LicenseServerCredential` flashaccess-tenant.xml文件中的元素。

   * 确保向提供当前凭证和旧凭证 `AsymmetricKeyRetrieval`

      * 在参考实施中，使用 `LicenseHandler.ServerCredential` 和 `AsymmetricKeyRetrieval.ServerCredential. n` 属性。

      * 在Primetime DRM Server for Protected Streaming中，旧凭据在 `LicenseServerCredential` flashaccess-tenant.xml文件中的元素。

   对于传输凭据：

   * 确保将当前凭据传递到 `HandlerConfiguration.setServerTransportCredential()` 方法：

      * 在参考实施中，使用 `HandlerConfiguration.ServerTransportCredential` 属性。
      * 在用于受保护流的Primetime DRM服务器中，当前凭据必须是中指定的第一个凭据 `TransportCredential` 中的元素 [!DNL flashaccess-tenant.xml] 文件。

   * 确保向提供旧凭据 `HandlerConfiguration.setAdditionalServerTransportCredentials`()：

      * 在参考实施中，使用 `HandlerConfiguration.AdditionalServerTransportCredential. n` 属性。
      * 在用于受保护流的Primetime DRM服务器中，将在中的第一个凭据之后指定 `TransportCredential` flashaccess-tenant.xml文件中的元素。

1. 更新打包工具，确保它们使用当前凭据打包内容。 请确保使用最新的许可证服务器证书、传输证书和打包程序凭据进行打包。
1. 按如下方式更新密钥服务器的许可证服务器证书：

   * 通过在flashaccess-keyserver-tenant.xml中包含旧密钥服务器凭据和新密钥服务器凭据，更新Adobe Primetime DRM Key Server租户配置文件中的凭据。
   * 确保将当前证书传递到 `HandlerConfiguration.setKeyServerCertificate()` 方法。

      * 在参考实施中，使用 `HandlerConfiguration.KeyServerCertificate` 属性。
      * 在用于受保护流的Primetime DRM服务器中，通过Configuration/Tenant/Certificates/KeyServer元素在中指定密钥服务器的证书。
