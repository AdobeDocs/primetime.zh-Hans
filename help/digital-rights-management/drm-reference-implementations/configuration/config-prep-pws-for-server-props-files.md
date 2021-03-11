---
title: 为服务器属性文件准备口令
description: 为服务器属性文件准备口令
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---


# 为服务器属性文件{#prepare-passwords-for-the-server-properties-files}准备口令

引用实现提供`ScrambleUtil.class`，一个类，用于确保凭据密码的安全性。

在将密码包含在[!DNL flashaccess-refimpl.properties]文件中之前，请使用此工具加密密码。

要运行该工具，您可以使用Ant脚本或Java。

实用程序会生成加密密码，必须将其复制到[!DNL flashaccess-refimpl.properties]文件。

>[!NOTE]
>
>已使用随参考实现提供的`ScrambleUtil.class`编码的密码不适用于受保护流的Primetime DRM服务器。
