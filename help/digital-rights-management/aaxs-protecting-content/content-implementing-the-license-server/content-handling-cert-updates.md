---
seo-title: 在Adobe颁发的证书过期时处理证书更新
title: 在Adobe颁发的证书过期时处理证书更新
uuid: 5151ef15-daf6-4fb3-bf83-25ebac1d003b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# 在Adobe颁发的证书过期{#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}时处理证书更新

有时您可能必须从Adobe获得新证书。 例如，当生产证书过期、评估证书过期或从评估切换到生产证书时。 当证书过期且您不希望重新打包使用旧证书的内容时。 您可以使许可证服务器同时了解新旧证书。

请按照以下过程使用新证书更新服务器：

1. （可选）在将新条目添加到现有策略更新列表或撤销列表时，请确保使用新凭据进行签名，并使用旧证书验证现有文件上的签名。

   例如，使用以下命令行向现有策略更新列表添加一个条目，该更新使用不同的凭据进行签名：

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

   在引用实现中，您使用的属性为`HandlerConfiguration.RevocationList`和`HandlerConfiguration.PolicyUpdateList`。 同时更新用于验证签名的证书：`RevocationList.verifySignature.X509Certificate`。

1. 要使用旧证书打包的内容，许可证服务器需要新旧许可证服务器凭据和传输凭据。 使用新旧证书更新许可证服务器。

   对于许可证服务器凭据：

   * 确保将当前凭据传递到`LicenseHandler`构造函数：

      * 在引用实现中，通过`LicenseHandler.ServerCredential`属性设置它。
      * 在“受保护流”的Adobe Access Server中，当前凭据必须是flashaccess-tenant.xml文件中`LicenseServerCredential`元素中指定的第一个凭据。
   * 确保向`AsymmetricKeyRetrieval`提供当前和旧凭据

      * 在引用实现中，通过`LicenseHandler.ServerCredential`和`AsymmetricKeyRetrieval.ServerCredential. n`属性设置它。
      * 在“受保护流”的Adobe Access Server中，旧凭据在flashaccess-tenant.xml文件的`LicenseServerCredential`元素中的第一个凭据之后指定。

   对于传输凭据：

   * 确保将当前凭据传递到`HandlerConfiguration.setServerTransportCredential()`方法：

      * 在引用实现中，通过`HandlerConfiguration.ServerTransportCredential`属性设置它。
      * 在受保护流的Adobe Access Server中，当前凭据必须是flashaccess-tenant.xml文件中`TransportCredential`元素中指定的第一个凭据。
   * 确保向`HandlerConfiguration.setAdditionalServerTransportCredentials`()提供旧凭据：

      * 在引用实现中，通过`HandlerConfiguration.AdditionalServerTransportCredential. n`属性设置它。
      * 在受保护流的Adobe Access Server中，这是在flashaccess-tenant.xml文件中`TransportCredential`元素中的第一个凭据之后指定的。




1. 更新打包工具，确保它们使用当前凭据打包内容。 确保使用最新的许可证服务器证书、传输证书和包装程序凭据进行打包。
1. 更新密钥服务器的许可证服务器证书：

   * 更新Adobe访问密钥服务器租户配置文件中的凭据。 在flashaccess-keyserver-tenant.xml中同时包含旧的和新的密钥服务器凭据。
   * 确保将当前证书传递到`HandlerConfiguration.setKeyServerCertificate()`方法。

      * 在引用实现中，通过`HandlerConfiguration.KeyServerCertificate`属性设置它。
      * 在“受保护流”的Adobe Access Server中，通过Configuration/Tenant/Certificates/KeyServer元素在中指定密钥服务器的证书。

