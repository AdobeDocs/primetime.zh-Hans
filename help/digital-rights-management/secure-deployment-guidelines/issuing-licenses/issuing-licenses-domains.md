---
description: 要防止用户备份和恢复文件以绕过域注销，您必须实施一些域管理方法。
title: 管理域
exl-id: cbf745d2-ba6e-4144-9608-23870bdfe16d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 管理域 {#managing-domains}

要防止用户备份和恢复文件以绕过域注销，您必须实施一些域管理方法。

以下是一些域管理方法：

* 限制域凭据的有效时间。

   当凭据过期时，客户端需要联系域服务器以重新获取域凭据。 此时，域服务器可以验证计算机是否仍被授权成为域的成员。
* 每次用户注销时滚动域密钥。

   许可证服务器应该只向拥有最新域密钥的客户端颁发许可证。 此方法假设许可证服务器可以与域服务器协调以确定哪个密钥是最新密钥。 对域密钥进行滚动涉及为域生成新的密钥对。 将鼠标指针置于域的键上时，将增加域的键版本 `generateDomainCredential`.
* 如果域服务器与许可证服务器相同，则服务器可以使用回滚计数器来检测备份和还原。

   有关更多信息，请参阅 [处理Adobe Primetime DRM请求](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).
