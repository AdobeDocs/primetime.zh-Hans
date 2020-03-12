---
description: 'null'
seo-description: 'null'
seo-title: 设置域服务器
title: 设置域服务器
uuid: bf85305e-9a00-4bc0-ba36-c870979456e4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 设置域服务器{#set-up-a-domain-server}

要在现有许可证服务器安装上配置域服务器，请执行以下操作：

1. 在目 [!DNL tomcat/lib] 录中，打开文 [!DNL flashaccess-refimpl.properties] 件。
1. 在选项 `Domain CA certificate` 下，填写域CA证书。

   然后，此证书用于接受域令牌。
1. 在选项 `Domain CA credential` 下，完成详细 `Domain CA credential certificate (PFX)` 信息。

   然后，此证书用于对域证书和令牌进行签名。
1. 为指定值 `DomainServerlURL`。

   如果将此值设置为， `NULL`则域身份验证可能会成功。 但是，在加入域时，可能会发生连接域错误。
