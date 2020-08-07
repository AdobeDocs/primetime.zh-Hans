---
seo-title: HSM配置
title: HSM配置
uuid: 1cc5be99-c24c-4c1e-9348-fb69f96d8ca5
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# HSM配置 {#hsm-configuration}

不需要使用HSM，但建议使用。 可以将引用实现配置为使用Sun PKCS11提供程序来支持HSM。 要在HSM上使用凭据，必须为Sun PKCS11提供程序创建配置文件。 有关详细信息，请参阅Sun文档。 要验证HSM和Sun PKCS11配置文件是否配置正确，可以使用以下命令（keytool随Java JDK一起安装）:

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

如果您在列表中看到凭据，则HSM配置正确。

>[!NOTE]
>
>自Java 1.7起，64位Sun Java for Windows不支持Adobe访问DRM与HSM设备通信所需的PKCS11接口。 如果您计划使用HSM，请使用32位版本的Java，或使用支持完整PKCS11接口的JDK。

