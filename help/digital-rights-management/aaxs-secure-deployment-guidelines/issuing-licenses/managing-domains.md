---
seo-title: 管理域
title: 管理域
uuid: aee02196-8704-46ee-add9-82b371722f0f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 管理域{#managing-domains}

为了防止用户在绕过域取消注册的情况下备份和恢复其文件，建议为域管理实施以下方法之一：

* 限制域凭据有效的时间。 客户端在过期时需要与域服务器联系才能重新获取域凭据。 此时，域服务器可以确保计算机仍被授权为域的成员。
* 每次用户取消注册时，将鼠标悬停在域键上。 许可证服务器仅应向具有最新域密钥的客户端发放许可证。 这假定许可证服务器可以与域服务器协作，以了解哪个密钥是最新的。 滚动域密钥涉及为域生成新密钥对。 滚动特定域的键时，请务必在中增加键版本 `generateDomainCredential`。 有关实现密钥转换的详细信息，请参 *阅“参考实施”中的RefImplDomainReqHandler* 。
* 如果域服务器与许可证服务器相同，则服务器可以使用回滚计数器检测备份和还原。 请参阅使用Adobe Access SDK保护内 *容中的*处理Adobe Access请求*。*

