---
title: HSM首选项
description: HSM首选项
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# HSM首选项{#hsm-preferences}

仅当在“打包程序”选项卡中选中&#x200B;**[!UICONTROL Enable HSM]**&#x200B;复选框时，才需要指定此选项卡中的首选项。 下表介绍了这些首选项：

| 首选项 | 说明 |
|---|---|
| Sun PKCS#11配置文件名 | Sun PKCS#11提供程序配置文件的完整路径。 有关此配置文件内容的详细信息，请参阅Sun网站上的Java PKCS#11参考指南。 |
| 分区密码 | 在PKCS#11配置文件中指定的HSM分区的口令。 |
| 许可证服务器证书别名 | 存储在HSM上的Adobe颁发的许可证服务器证书的别名。 此证书用于在打包期间加密CEK。 在Packager选项卡中指定此选项，而不是&#x200B;*许可证服务器证书*。 |
| 许可证服务器传输证书别名 | 存储在HSM上的Adobe颁发的服务器传输证书的别名。 此证书用于保护客户端和许可证服务器之间的通信。 在Packager选项卡中指定此选项，而不是&#x200B;*许可证服务器传输证书*。 |
| Packager凭据别名 | 存储在HSM上的Adobe颁发的打包程序凭据（证书和私钥）的别名。 这用于在打包期间对元数据进行签名。 在Packager选项卡中指定此值，而不是&#x200B;*Packager Credential*。 |
| 许可证服务器凭据别名 | 存储在HSM上的Adobe颁发的许可证服务器凭据（证书和私钥）的别名。 此凭据用于签署策略更新列表。 在“策略更新”列表卡中指定此选项，而不是&#x200B;*许可证服务器凭据*。 （此别名可能与&#x200B;*许可证服务器证书别名*&#x200B;相同。） |

