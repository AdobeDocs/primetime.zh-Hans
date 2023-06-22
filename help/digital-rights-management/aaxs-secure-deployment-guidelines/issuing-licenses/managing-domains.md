---
title: 管理域
description: 管理域
copied-description: true
exl-id: c9030373-fd54-4745-9f03-0218532b9d6d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 管理域{#managing-domains}

为了防止用户备份和恢复其文件以绕过域注销，建议对域管理实施以下方法之一：

* 限制域凭据的有效时间。 客户端需要联系域服务器以在过期时重新获取域凭据。 此时，域服务器可以确保计算机仍被授权成为域的成员。
* 当用户每次取消注册时，将域密钥滚动。 许可证服务器应该只向拥有最新域密钥的客户端颁发许可证。 这假定许可证服务器可以与域服务器协调以确定哪个密钥是最新密钥。 对域密钥进行滚动涉及为域生成新的密钥对。 将鼠标指针置于特定域的键上时，请务必增加中的键版本 `generateDomainCredential`. 有关实施密钥滚动更新的更多信息，请参阅 *RefImplDomainReqHandler* 在参考实施中。
* 如果域服务器与许可证服务器相同，则服务器可以使用回滚计数器来检测备份和还原。 请参阅*中的*处理Adobe访问请求* *使用Adobe访问SDK保护内容。*
