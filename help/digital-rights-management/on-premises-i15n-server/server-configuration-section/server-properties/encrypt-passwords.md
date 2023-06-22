---
title: 加密密码
description: 加密密码
copied-description: true
exl-id: 97b78e00-e5e3-4a9d-8eab-fcf96d3b1219
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 0%

---

# 加密密码{#encrypt-passwords}

属性文件包含多个密码值，您不能以纯文本形式输入这些值。 使用以下命令加密这些值：

`java -jar adobe-flashaccess-i15n-setup.jar password`

此命令将输出一个加密的密码，然后您可以在属性文件中使用该密码。

>[!NOTE]
>这不是用于加密许可证服务器密码的实用程序。
