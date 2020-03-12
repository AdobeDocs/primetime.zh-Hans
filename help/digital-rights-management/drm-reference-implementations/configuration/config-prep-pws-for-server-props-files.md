---
description: 'null'
seo-description: 'null'
seo-title: 为服务器属性文件准备口令
title: 为服务器属性文件准备口令
uuid: 3e00ba9b-b692-4713-8306-5ab896461f2a
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 为服务器属性文件准备口令{#prepare-passwords-for-the-server-properties-files}

引用实现提 `ScrambleUtil.class`供一个类，它确保凭据密码的安全性。

在将密码包含在文件中之前，使用此工具加密该密 [!DNL flashaccess-refimpl.properties] 码。

要运行该工具，您可以使用Ant脚本或Java。

该实用程序会生成加密密码，您必须将其复制到文 [!DNL flashaccess-refimpl.properties] 件中。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>已使用随参考实现提 `ScrambleUtil.class` 供的密码进行编码的密码不适用于Primetime DRM Server for Protected Streaming。
