---
description: 'null'
seo-description: 'null'
seo-title: 为服务器属性文件准备口令
title: 为服务器属性文件准备口令
uuid: 3e00ba9b-b692-4713-8306-5ab896461f2a
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 为服务器属性文件准备口令{#prepare-passwords-for-the-server-properties-files}

引用实现提供`ScrambleUtil.class`，一个类，它确保凭据密码的安全性。

在将密码包含在[!DNL flashaccess-refimpl.properties]文件中之前，使用此工具对密码进行加密。

要运行该工具，您可以使用Ant脚本或Java。

该实用程序生成加密密码，必须将其复制到[!DNL flashaccess-refimpl.properties]文件。

>[!NOTE]
>
>已使用随参考实现提供的`ScrambleUtil.class`进行编码的密码不适用于Primetime DRM Server for Protected Streaming。
