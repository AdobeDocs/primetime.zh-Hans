---
title: HSM配置
description: HSM配置
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# HSM配置 {#hsm-configuration}

如果您选择使用HSM来存储您的服务器凭据，则必须将私钥和证书加载到HSM上并创建 [!DNL pkcs11.cfg] 配置文件。 该文件必须位于 *LicenseServer.ConfigRoot* 目录。 请参阅 [!DNL Adobe Access Server for Protected Streaming/configs] Adobe访问DVD上的目录，例如PKCS11配置文件。 有关格式的信息 [!DNL pkcs11.cfg]，请参见Sun PKCS11提供程序文档。

要验证HSM和Sun PKCS11配置文件是否正确配置，可以使用以下目录中的命令： [!DNL pkcs11.cfg] 文件位于( [!DNL keytool] 随Java JRE和JDK一起安装)：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果在列表中看到您的凭据，则HSM配置正确，许可证服务器将能够访问凭据。

>[!NOTE]
>
>用于受保护流的Adobe访问服务器当前不支持64位Windows操作系统上的HSM。
