---
description: 可以使用支持HSM的Sun PKCS#11提供程序配置引用实现。 虽然HSM不是必需的，但建议使用。
seo-description: 可以使用支持HSM的Sun PKCS#11提供程序配置引用实现。 虽然HSM不是必需的，但建议使用。
seo-title: HSM配置
title: HSM配置
uuid: 2741ac40-aa42-4aa7-9864-037f3ed3dee2
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# HSM配置{#hsm-configuration}

可以使用支持HSM的Sun PKCS#11提供程序配置引用实现。 虽然HSM不是必需的，但建议使用。

要在HSM上使用凭据，必须为Sun PKCS#11提供者创建配置文件。 有关详细信息，请参 [阅Java PCKS#11参考指南](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html)。

要验证您的HSM和Sun PKCS#11配置文件是否已配置，请使用随Java JDK一起安装的keytool键入以下命令：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您可以在列表中查看凭据，则您已正确配置了HSM。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>自Java 1.7起，64位Sun Java for Windows不再支持Adobe Primetime DRM与HSM设备通信所需的PKCS#11接口。 如果您计划使用HSM，请确保使用32位版本的Java或使用支持完整PKCS#11接口的JDK。

