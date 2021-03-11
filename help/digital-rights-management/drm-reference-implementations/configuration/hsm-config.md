---
description: 您可以使用支持HSM的Sun PKCS#11提供程序配置引用实现。 虽然不需要使用HSM，但建议使用。
title: HSM配置
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# HSM配置{#hsm-configuration}

您可以使用支持HSM的Sun PKCS#11提供程序配置引用实现。 虽然不需要使用HSM，但建议使用。

要在HSM上使用凭据，必须为Sun PKCS#11提供程序创建配置文件。 有关详细信息，请参阅[Java PCKS#11参考指南](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html)。

要验证是否配置了HSM和Sun PKCS#11配置文件，请使用随Java JDK一起安装的keytool键入以下命令：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果可以在列表中视图凭据，则您已正确配置了HSM。

>[!NOTE]
>
>自Java 1.7起，64位Sun Java for Windows不再支持Adobe Primetime DRM与HSM设备通信所需的PKCS#11接口。 如果您计划使用HSM，请确保使用32位版本的Java或使用支持完整PKCS#11接口的JDK。

