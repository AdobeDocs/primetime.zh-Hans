---
description: 如果选择HSM来存储服务器凭据，则必须将私钥和证书加载到HSM上并创建pkcs11.cfg配置文件。
title: HSM配置
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# HSM配置{#hsm-configuration}

如果选择HSM来存储服务器凭据，则必须将私钥和证书加载到HSM上并创建pkcs11.cfg配置文件。

您必须在以下位置找到配置文件： *LicenseServer.ConfigRoot* 目录。

请参阅 [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] Adobe Primetime DRM DVD上的目录，例如PKCS11配置文件。

有关格式的信息，请参见Sun PKCS11提供程序文档 [!DNL pkcs11.cfg] 文件。

您可以从以下目录中使用以下命令： [!DNL pkcs11.cfg] 文件位于( [!DNL keytool] Java JRE和JDK一起安装)，以验证是否已正确配置HSM和Sun PKCS11配置文件：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您可以在列表中查看您的凭据，那么HSM已正确配置，许可证服务器现在可以访问凭据。
