---
seo-title: HSM配置
title: HSM配置
uuid: da4d7118-65a8-460d-a796-b7bf5c28b208
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9

---


# HSM配置 {#hsm-configuration}

如果选择使用HSM存储服务器凭据，则必须将私钥和证书加载到HSM上并创建配 [!DNL pkcs11.cfg] 置文件。 此文件必须位于 *LicenseServer.ConfigRoot目录中* 。 有关PKCS11 [!DNL Adobe Access Server for Protected Streaming/configs] 配置文件示例，请参阅Adobe Access DVD上的目录。 有关格式的信息，请 [!DNL pkcs11.cfg]参阅Sun PKCS11提供商文档。

要验证HSM和Sun PKCS11配置文件是否正确配置，可以从文件所在的目录（随Java JRE和JDK一起安装）中使用以 [!DNL pkcs11.cfg] 下命 [!DNL keytool] 令：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您在列表中看到凭据，则HSM配置正确，许可证服务器将能够访问凭据。

> [!NOTE]
> 用于受保护流的Adobe Access Server当前不支持64位Windows OS上的HSM。

