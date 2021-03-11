---
title: Adobe访问凭据
description: Adobe访问凭据
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Adobe访问凭据{#adobe-access-credentials}

要颁发Adobe Access客户端接受的有效许可证，Adobe Access Server的受保护流必须配置由Adobe颁发的一组凭据。 这些凭据可以存储在PKCS#12(.pfx)文件中或存储在HSM中。

.pfx文件可能位于任何位置，但为便于配置，我们建议将.pfx文件放在租户的配置目录中。 有关详细信息，请参阅“[许可证服务器配置文件](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)”。