---
description: 如果选择HSM来存储服务器凭据，则必须将私钥和证书加载到HSM上并创建pkcs11.cfg配置文件。
seo-description: 如果选择HSM来存储服务器凭据，则必须将私钥和证书加载到HSM上并创建pkcs11.cfg配置文件。
seo-title: HSM配置
title: HSM配置
uuid: 3610840b-082e-4a73-8aa5-5065f9232e0b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# HSM配置{#hsm-configuration}

如果选择HSM来存储服务器凭据，则必须将私钥和证书加载到HSM上并创建pkcs11.cfg配置文件。

必须在&#x200B;*LicenseServer.ConfigRoot*&#x200B;目录中找到配置文件。

有关PKCS11配置文件的示例，请参阅Adobe PrimetimeDRM DVD上的[!DNL Adobe Primetime DRM Server for Protected Streaming/configs]目录。

请参阅Sun PKCS11提供程序文档，其中介绍了[!DNL pkcs11.cfg]文件的格式。

您可以从[!DNL pkcs11.cfg]文件所在的目录（[!DNL keytool]随Java JRE和JDK一起安装）中使用以下命令来验证HSM和Sun PKCS11配置文件是否已正确配置：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您可以在列表中视图凭据，则HSM配置正确，许可证服务器现在可以访问凭据。
