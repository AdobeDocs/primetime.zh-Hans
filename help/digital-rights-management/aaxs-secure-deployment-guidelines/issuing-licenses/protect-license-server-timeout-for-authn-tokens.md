---
seo-title: 身份验证令牌超时
title: 身份验证令牌超时
uuid: 41b0fbf5-a567-4118-bec1-c05e6e0b6d1f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 身份验证令牌超时{#timeout-for-authentication-tokens}

Adobe Access SDK生成的所有身份验证令牌都有一个超时间隔，以保护应用程序安全。 在处理身份验证请求时，使用Adobe Access SDK指定身份验证令牌的过期时间。 到期后，身份验证令牌不再有效，用户必须使用许可证服务器重新进行身份验证。

要了解有关身份验证请求的更多信息，请参阅 *Adobe Access API参考中的AuthenticationHandler*。
