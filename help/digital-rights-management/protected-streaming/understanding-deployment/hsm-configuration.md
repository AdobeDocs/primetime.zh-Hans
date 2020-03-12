---
description: 如果选择HSM来存储服务器凭据，则必须将私钥和证书加载到HSM上并创建pkcs11.cfg配置文件。
seo-description: 如果选择HSM来存储服务器凭据，则必须将私钥和证书加载到HSM上并创建pkcs11.cfg配置文件。
seo-title: HSM配置
title: HSM配置
uuid: 3610840b-082e-4a73-8aa5-5065f9232e0b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# HSM配置{#hsm-configuration}

如果选择HSM来存储服务器凭据，则必须将私钥和证书加载到HSM上并创建pkcs11.cfg配置文件。

必须在 *LicenseServer.ConfigRoot目录中找到配置文* 件。

有关 [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] PKCS11配置文件示例，请参阅Adobe Primetime DRM DVD上的目录。

请参阅Sun PKCS11提供商关于文件格式的 [!DNL pkcs11.cfg] 文档。

可以从文件所在的目录(随 [!DNL pkcs11.cfg][!DNL keytool] Java JRE和JDK一起安装)中使用以下命令来验证HSM和Sun PKCS11配置文件是否已正确配置：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您可以在列表中查看凭据，则HSM配置正确，许可证服务器现在可以访问凭据。
