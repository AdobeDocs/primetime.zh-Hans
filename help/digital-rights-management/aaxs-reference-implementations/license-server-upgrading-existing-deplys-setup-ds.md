---
title: 设置域服务器
description: 设置域服务器
copied-description: true
exl-id: b2589412-25e4-44c8-be11-8b2cfccbf7bb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 设置域服务器 {#set-up-a-domain-server}

要在现有许可证服务器安装中配置域服务器，请执行以下任务：

1. 打开 [!DNL flashaccess-refimpl.properties] 文件位于 [!DNL tomcat/lib].

1. 在 `Domain CA certificate` 选项，填写域CA证书详细信息。 此证书将用于接受域令牌。
1. 在 `Domain CA credential` 选项，请填写 `Domain CA credential certificate (PFX)` 详细信息。 此证书将用于签署域证书和令牌。

1. 指定值 `DomainServerlURL`. 如果此值为NULL，域身份验证可能会成功。 但是，在加入域时，会出现加入域错误。
