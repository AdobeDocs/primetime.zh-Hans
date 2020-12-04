---
seo-title: HSM配置
title: HSM配置
uuid: da4d7118-65a8-460d-a796-b7bf5c28b208
translation-type: tm+mt
source-git-commit: ac75f63f98060e1937570476362bb5d4458d1f85
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# HSM配置{#hsm-configuration}

如果选择使用HSM存储服务器凭据，则必须将私钥和证书加载到HSM上并创建[!DNL pkcs11.cfg]配置文件。 此文件必须位于&#x200B;*LicenseServer.ConfigRoot*&#x200B;目录中。 有关PKCS11配置文件的示例，请参阅Adobe访问DVD上的[!DNL Adobe Access Server for Protected Streaming/configs]目录。 有关[!DNL pkcs11.cfg]格式的信息，请参阅Sun PKCS11提供程序文档。

要验证HSM和Sun PKCS11配置文件配置是否正确，可以从[!DNL pkcs11.cfg]文件所在的目录（[!DNL keytool]随Java JRE和JDK一起安装）使用以下命令：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您在列表中看到凭据，则HSM配置正确，许可证服务器将能够访问凭据。

>[!NOTE]
>
>Adobe访问服务器当前不支持64位Windows OS上的HSM。
