---
description: 'null'
seo-description: 'null'
seo-title: 设置域服务器
title: 设置域服务器
uuid: bf85305e-9a00-4bc0-ba36-c870979456e4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# 设置域服务器{#set-up-a-domain-server}

在现有许可证服务器安装上配置域服务器：

1. 在[!DNL tomcat/lib]目录中，打开[!DNL flashaccess-refimpl.properties]文件。
1. 在`Domain CA certificate`选项下，完成域CA证书。

   然后，此证书用于接受域令牌。
1. 在`Domain CA credential`选项下，完成`Domain CA credential certificate (PFX)`详细信息。

   然后，此证书用于对域证书和令牌进行签名。
1. 指定`DomainServerlURL`的值。

   如果此值设置为`NULL`，则域身份验证可能成功。 但是，加入域时，可能会发生加入域错误。
