---
description: 可以使用支持HSM的Sun PKCS#11提供程序配置参考实施。 虽然不要求使用HSM，但建议使用HSM。
title: HSM配置
exl-id: 87a7d242-8202-4749-91a6-e6697be6a61d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# HSM配置{#hsm-configuration}

可以使用支持HSM的Sun PKCS#11提供程序配置参考实施。 虽然不要求使用HSM，但建议使用HSM。

要在HSM上使用凭据，必须为Sun PKCS#11提供程序创建配置文件。 欲了解更多信息，请参见 [Java PCKS#11参考指南](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html).

要验证是否已配置HSM和Sun PKCS#11配置文件，请使用随Java JDK一起安装的keytool键入以下命令：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您可以在列表中查看凭据，则表明已正确配置HSM。

>[!NOTE]
>
>从Java 1.7开始，适用于Windows的64位Sun Java不再支持Adobe Primetime DRM与HSM设备通信所需的PKCS#11接口。 如果您计划使用HSM，请确保您使用32位版本的Java或使用支持完整PKCS#11接口的JDK。
