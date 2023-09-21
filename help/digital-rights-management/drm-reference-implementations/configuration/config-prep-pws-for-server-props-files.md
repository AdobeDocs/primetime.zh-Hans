---
title: 为服务器属性文件准备密码
description: 为服务器属性文件准备密码
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 为服务器属性文件准备密码{#prepare-passwords-for-the-server-properties-files}

参考实施提供了 `ScrambleUtil.class`，确保凭据密码安全的类。

使用此工具先加密密码，然后再将其包含到 [!DNL flashaccess-refimpl.properties] 文件。

要运行该工具，可以使用Ant脚本或Java。

该实用程序将生成加密的密码，您必须将其复制到 [!DNL flashaccess-refimpl.properties] 文件。

>[!NOTE]
>
>已使用编码的密码 `ScrambleUtil.class` 参考实施中提供的服务器不能用于Primetime DRM Server for Protected Streaming。
