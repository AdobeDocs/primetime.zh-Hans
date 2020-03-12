---
seo-title: 加密口令
title: 加密口令
uuid: 94dc7fe9-fe40-4779-912a-d84b58e4ee36
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c

---


# 加密口令{#encrypt-passwords}

属性文件包含多个不应以纯文本形式输入的口令值。 使用以下命令加密这些值：

`java -jar adobe-flashaccess-i15n-setup.jar password`

此命令将输出加密密码，然后在属性文件中使用。

>[!NOTE]
>这不是用于加密许可证服务器密码的实用程序。

