---
title: HSM配置
description: HSM配置
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# HSM配置 {#hsm-configuration}

不需要使用HSM，但建议使用。 可以将参考实现配置为使用Sun PKCS11提供程序来支持HSM。 要在HSM上使用凭据，必须为Sun PKCS11提供程序创建配置文件。 有关详细信息，请参见Sun文档。 要验证是否已正确配置HSM和Sun PKCS11配置文件，可以使用以下命令（Java JDK中安装了keytool）：

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

如果在列表中看到您的凭据，则表示HSM已正确配置。

>[!NOTE]
>
>从Java 1.7开始，用于Windows的64位Sun Java不支持Adobe访问DRM与HSM设备通信所需的PKCS11接口。 如果您计划使用HSM，请使用32位版本的Java，或使用支持完整PKCS11接口的JDK。
