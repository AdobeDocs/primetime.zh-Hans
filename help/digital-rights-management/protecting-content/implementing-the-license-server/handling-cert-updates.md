---
title: 在Adobe颁发的证书过期时处理证书更新
description: 在Adobe颁发的证书过期时处理证书更新
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# 在Adobe颁发的证书过期{#handling-certificate-updates-when-adobe-issued-certificates-expire}时处理证书更新

您可能需要从Adobe获得新证书。 例如，当评估证书过期或从评估证书切换到生产证书时，生产证书将过期。 只要证书过期，而您不希望重新打包使用旧证书的内容，您就可以使许可证服务器同时识别旧证书和新证书。

使用新证书更新服务器：

1. （可选）在将新条目添加到现有DRM策略更新列表或吊销列表时，您需要使用新凭据进行签名，并使用旧证书验证现有文件上的签名。

   例如，您可以使用以下命令行向现有DRM策略更新列表添加一个条目，该条目已使用其他凭据进行签名：

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

   在引用实现中，您使用的属性为`HandlerConfiguration.RevocationList`和`HandlerConfiguration.PolicyUpdateList`。 您还需要更新用于验证签名的证书：`RevocationList.verifySignature.X509Certificate`。

1. 使用新旧证书更新许可证服务器。

   如果要使用使用旧证书打包的内容，请确保许可证服务器有权访问新旧许可证服务器凭据以及传输凭据。

   对于许可证服务器凭据：

   * 确保将当前凭据传递到`LicenseHandler`构造函数：

      * 在引用实现中，使用`LicenseHandler.ServerCredential`属性设置它。
      * 在Adobe Primetime DRM Server的受保护流中，当前凭据必须是flashaccess-tenant.xml文件中`LicenseServerCredential`元素中指定的第一个凭据。
   * 确保向`AsymmetricKeyRetrieval`提供当前和旧凭据

      * 在引用实现中，使用`LicenseHandler.ServerCredential`和`AsymmetricKeyRetrieval.ServerCredential. n`属性设置它。

      * 在Primetime DRM Server的受保护流中，旧凭据是在flashaccess-tenant.xml文件中`LicenseServerCredential`元素中的第一个凭据之后指定的。

   对于传输凭据：

   * 确保将当前凭据传递到`HandlerConfiguration.setServerTransportCredential()`方法：

      * 在引用实现中，使用`HandlerConfiguration.ServerTransportCredential`属性设置它。
      * 在Primetime DRM Server中，对于受保护的流，当前凭据必须是[!DNL flashaccess-tenant.xml]文件中`TransportCredential`元素中指定的第一个凭据。
   * 确保向`HandlerConfiguration.setAdditionalServerTransportCredentials`()提供旧凭据：

      * 在引用实现中，使用`HandlerConfiguration.AdditionalServerTransportCredential. n`属性设置它。
      * 在Primetime DRM Server中，这是在flashaccess-tenant.xml文件中`TransportCredential`元素中的第一个凭据之后指定的。




1. 更新打包工具，确保它们使用当前凭据打包内容。 确保使用最新的许可证服务器证书、传输证书和打包程序凭据进行打包。
1. 按如下方式更新密钥服务器的许可证服务器证书：

   * 通过在flashaccess-keyserver-tenant.xml中同时包含旧的和新的Key Server凭据，更新Adobe Primetime DRM Key Server租户配置文件中的凭据。
   * 确保将当前证书传递到`HandlerConfiguration.setKeyServerCertificate()`方法。

      * 在引用实现中，使用`HandlerConfiguration.KeyServerCertificate`属性设置它。
      * 在用于受保护流的Primetime DRM服务器中，通过Configuration/Tenant/Certificates/KeyServer元素在中指定Key Server的证书。

