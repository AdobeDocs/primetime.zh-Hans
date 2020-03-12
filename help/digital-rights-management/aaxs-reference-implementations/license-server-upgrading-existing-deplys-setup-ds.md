---
seo-title: 设置域服务器
title: 设置域服务器
uuid: b262ea86-f465-4ed1-b278-122d4dafc881
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 设置域服务器 {#set-up-a-domain-server}

要在现有许可证服务器安装上配置域服务器，请执行以下任务：

1. 在下面打 [!DNL flashaccess-refimpl.properties] 开文件 [!DNL tomcat/lib]。

1. 在选项 `Domain CA certificate` 下，填写域CA证书详细信息。 此证书将用于接受域令牌。
1. 在选 `Domain CA credential` 项下，填写详细 `Domain CA credential certificate (PFX)` 信息。 此证书将用于对域证书和令牌进行签名。

1. 为指定值 `DomainServerlURL`。 如果此值为NULL，则域身份验证可能成功。 但是，在加入域时，将出现连接域错误。

