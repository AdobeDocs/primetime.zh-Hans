---
title: 加密口令
description: 加密口令
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 0%

---


# 加密口令{#encrypt-passwords}

属性文件包含多个不应以纯文本形式输入的口令值。 使用以下命令加密这些值：

`java -jar adobe-flashaccess-i15n-setup.jar password`

此命令将输出加密密码，然后在属性文件中使用。

>[!NOTE]
>这不是用于加密许可证服务器密码的实用程序。

