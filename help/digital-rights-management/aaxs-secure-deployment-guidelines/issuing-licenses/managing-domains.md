---
title: 管理域
description: 管理域
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# 管理域{#managing-domains}

为防止用户为了绕过域取消注册而备份和恢复其文件，建议对域管理实施以下方法之一：

* 限制域凭据有效的时间。 客户端需要与域服务器联系，以在域证书过期时重新获取域凭据。 此时，域服务器可以确保计算机仍被授权为域的成员。
* 每次用户取消注册时，滚动域键。 许可证服务器应仅向具有最新域密钥的客户端颁发许可证。 这假定许可证服务器可以与域服务器协作，以了解最新的密钥。 滚动域密钥涉及为域生成新密钥对。 滚动到特定域的键时，请确保在`generateDomainCredential`中增加键版本。 有关实现密钥转换的详细信息，请参阅“参考实现”中的&#x200B;*RefImplDomainReqHandler*。
* 如果域服务器与许可证服务器相同，则服务器可以使用回滚计数器检测备份和恢复。 请参阅&#x200B;*使用Adobe Access SDK保护内容中的*处理Adobe访问请求*。*

