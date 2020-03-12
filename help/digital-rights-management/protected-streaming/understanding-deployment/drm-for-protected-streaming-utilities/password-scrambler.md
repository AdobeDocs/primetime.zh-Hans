---
description: Password Scrambler实用程序为Adobe Primetime DRM Server的受保护流配置文件加密密码。
seo-description: Password Scrambler实用程序为Adobe Primetime DRM Server的受保护流配置文件加密密码。
seo-title: 密码剪贴器
title: 密码剪贴器
uuid: 56df0f49-f3fd-464d-b4ba-25e1b497158a
translation-type: tm+mt
source-git-commit: 105dedcfe47a5f454a067e66a95827e638290742

---


# 密码剪贴器 {#password-scrambler}

Password Scrambler实用程序为Adobe Primetime DRM Server的受保护流配置文件加密密码。

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

您在和文件中指定的所 [!DNL flashaccess-global.xml] 有密 [!DNL flashaccess-tenant.xml] 码都必须加密。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Primetime DRM Server中用于受保护流的密码扰码器实用程序不能与随参考实施许可服务器提供的扰码器互换。