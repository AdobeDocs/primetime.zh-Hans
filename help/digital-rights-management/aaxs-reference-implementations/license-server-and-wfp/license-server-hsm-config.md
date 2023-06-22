---
title: HSM配置
description: HSM配置
copied-description: true
exl-id: 0418bcc1-0a85-4074-9616-915f77507bdd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# HSM配置 {#hsm-configuration}

不要求使用HSM，但建议使用。 参考实施可以配置为使用Sun PKCS11提供程序来支持HSM。 要在HSM上使用凭据，必须为Sun PKCS11提供程序创建配置文件。 有关详细信息，请参见Sun文档。 要验证HSM和Sun PKCS11配置文件是否正确配置，可以使用以下命令（keytool随Java JDK一起安装）：

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

如果在列表中看到您的凭据，则表示HSM已正确配置。

>[!NOTE]
>
>从Java 1.7开始，64位Sun Java for Windows不支持Adobe访问DRM与HSM设备通信所需的PKCS11接口。 如果您计划使用HSM，请使用32位版本的Java，或使用支持完整PKCS11接口的JDK。
