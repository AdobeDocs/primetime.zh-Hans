---
title: 设置域服务器
description: 设置域服务器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# 设置域服务器{#set-up-a-domain-server}

要在现有许可证服务器安装上配置域服务器，请执行以下任务:

1. 打开[!DNL tomcat/lib]下的[!DNL flashaccess-refimpl.properties]文件。

1. 在`Domain CA certificate`选项下，填写域CA证书详细信息。 此证书将用于接受域令牌。
1. 在`Domain CA credential`选项下，填写`Domain CA credential certificate (PFX)`详细信息。 此证书将用于对域证书和令牌进行签名。

1. 指定`DomainServerlURL`的值。 如果此值为NULL，则域身份验证可能成功。 但是，加入域时，将出现加入域错误。

