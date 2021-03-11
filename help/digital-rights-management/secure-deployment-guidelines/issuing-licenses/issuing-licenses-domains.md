---
description: 要阻止用户备份和恢复文件以绕过域取消注册，必须实施一些域管理方法。
title: 管理域
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# 管理域{#managing-domains}

要阻止用户备份和恢复文件以绕过域取消注册，必须实施一些域管理方法。

以下是一些域管理方法：

* 限制域凭据有效的时间。

   当凭据过期时，客户端需要与域服务器联系以重新获取域凭据。 此时，域服务器可以验证计算机是否仍被授权为域的成员。
* 每次用户注销时，滚动到域密钥上。

   许可证服务器应仅向具有最新域密钥的客户端颁发许可证。 此方法假定许可证服务器可以与域服务器协调，以了解哪个密钥是最新的。 滚动域密钥涉及为域生成新密钥对。 滚动到域的键时，请增加`generateDomainCredential`中的键版本。
* 如果域服务器与许可证服务器相同，则服务器可以使用回滚计数器检测备份和还原。

   有关详细信息，请参阅[处理Adobe Primetime DRM请求](../../protecting-content/implementing-the-license-server/processing-drm-requests.md)。

