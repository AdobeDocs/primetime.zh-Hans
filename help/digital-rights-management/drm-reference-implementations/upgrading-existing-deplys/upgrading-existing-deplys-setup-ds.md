---
title: 设置域服务器
description: 设置域服务器
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# 设置域服务器{#set-up-a-domain-server}

要在现有许可证服务器安装中配置域服务器，请执行以下操作：

1. 在 [!DNL tomcat/lib] 目录，打开 [!DNL flashaccess-refimpl.properties] 文件。
1. 在 `Domain CA certificate` 选项，完成域CA证书。

   然后，使用此证书来接受域令牌。
1. 在 `Domain CA credential` 选项，填写 `Domain CA credential certificate (PFX)` 详细信息。

   然后，此证书用于签名域证书和令牌。
1. 指定值 `DomainServerlURL`.

   如果此值设置为 `NULL`，域身份验证可能会成功。 但是，在加入域时，可能会发生加入域错误。
