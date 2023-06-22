---
description: Password Scrambler实用程序用于加密Adobe Primetime DRM Server for Protected Streaming配置文件的密码。
title: 密码加扰器
exl-id: 9cedd3e5-01db-4ea9-bf23-8767987fc26c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 密码加扰器 {#password-scrambler}

Password Scrambler实用程序用于加密Adobe Primetime DRM Server for Protected Streaming配置文件的密码。

要运行扰频器，请键入：

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

该实用程序显示以下消息：

```
Encrypted password:  
<i class="+ topic ph hi-d="" i "="">
  scrambled-password 
</i class="+ topic>
```

您在 [!DNL flashaccess-global.xml] 和 [!DNL flashaccess-tenant.xml] 文件必须加密。

>[!NOTE]
>
>用于受保护流的Primetime DRM服务器中的密码扰码器实用程序不能与参考实现许可证服务器提供的扰码器互换。
