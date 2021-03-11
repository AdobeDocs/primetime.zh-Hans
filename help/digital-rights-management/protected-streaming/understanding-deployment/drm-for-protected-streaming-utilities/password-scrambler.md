---
description: 密码剪贴器实用程序为Adobe Primetime DRM Server的受保护流配置文件加密密码。
title: 密码剪贴器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# 密码剪贴器{#password-scrambler}

密码剪贴器实用程序为Adobe Primetime DRM Server的受保护流配置文件加密密码。

要运行剪贴器，请键入：

```
Scrambler.bat  
<i class="+ topic ph hi-d="" i "="">
  password 
</i class="+ topic>
```

或

```
java -jar libs/flashaccess-scrambler.jar  
<i class="+ topic ph hi-d="" i "="">
  password  
</i class="+ topic>
```

实用程序显示以下消息：

```
Encrypted password:  
<i class="+ topic ph hi-d="" i "="">
  scrambled-password 
</i class="+ topic>
```

必须在[!DNL flashaccess-global.xml]和[!DNL flashaccess-tenant.xml]文件中指定的所有口令都必须加密。

>[!NOTE]
>
>Primetime DRM Server for Protected Streaming中的密码扰码器实用程序不能与随参考实施许可证服务器提供的扰码器互换。