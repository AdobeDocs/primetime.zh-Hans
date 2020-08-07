---
description: 密码扰码器实用程序加密Adobe PrimetimeDRM服务器的受保护流配置文件的密码。
seo-description: 密码扰码器实用程序加密Adobe PrimetimeDRM服务器的受保护流配置文件的密码。
seo-title: 密码剪贴器
title: 密码剪贴器
uuid: 56df0f49-f3fd-464d-b4ba-25e1b497158a
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---


# 密码剪贴器 {#password-scrambler}

密码扰码器实用程序加密Adobe PrimetimeDRM服务器的受保护流配置文件的密码。

要运行剪贴机，请键入：

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

您在和文件中指定的所 [!DNL flashaccess-global.xml] 有口 [!DNL flashaccess-tenant.xml] 令必须加密。

>[!NOTE]
>
>Primetime DRM Server中用于受保护流的密码扰码器实用程序不能与随参考实施许可证服务器提供的扰码器互换。