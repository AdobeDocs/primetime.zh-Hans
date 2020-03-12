---
description: 要阻止用户备份和恢复文件以绕过域取消注册，您必须实施一些域管理方法。
seo-description: 要阻止用户备份和恢复文件以绕过域取消注册，您必须实施一些域管理方法。
seo-title: 管理域
title: 管理域
uuid: 30b73e38-d6ed-43c6-89ba-ae8616383779
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 管理域 {#managing-domains}

要阻止用户备份和恢复文件以绕过域取消注册，您必须实施一些域管理方法。

以下是一些域管理方法：

* 限制域凭据有效的时间。

   客户端需要与域服务器联系，以在凭据过期时重新获取域凭据。 此时，域服务器可以验证计算机是否仍被授权为域的成员。
* 每次用户取消注册时，滚动到域键上。

   许可证服务器仅应向具有最新域密钥的客户端发放许可证。 此方法假定许可证服务器可以与域服务器协作，以了解最新的密钥。 滚动域密钥涉及为域生成新密钥对。 滚动到域的键上时，请增加中的键版本 `generateDomainCredential`。
* 如果域服务器与许可证服务器相同，则服务器可以使用回滚计数器检测备份和恢复。

   有关详细信息，请参 [阅处理Adobe Primetime DRM请求](../../protecting-content/implementing-the-license-server/processing-drm-requests.md)。

