---
title: 设置域服务器
description: 设置域服务器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---


# 设置域服务器{#set-up-a-domain-server}

要在现有许可证服务器安装上配置域服务器，请执行以下操作：

1. 在[!DNL tomcat/lib]目录中，打开[!DNL flashaccess-refimpl.properties]文件。
1. 在`Domain CA certificate`选项下，完成域CA证书。

   然后，此证书用于接受域令牌。
1. 在`Domain CA credential`选项下，完成`Domain CA credential certificate (PFX)`详细信息。

   然后，此证书用于对域证书和令牌进行签名。
1. 指定`DomainServerlURL`的值。

   如果将此值设置为`NULL`，则域身份验证可能会成功。 但是，加入域时，可能会发生加入域错误。
