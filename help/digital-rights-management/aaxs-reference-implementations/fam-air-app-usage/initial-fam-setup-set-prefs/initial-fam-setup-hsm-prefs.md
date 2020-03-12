---
seo-title: HSM首选项
title: HSM首选项
uuid: 1b97d582-d4b6-48cd-9c24-2d13493571e9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# HSM首选项 {#hsm-preferences}

仅当在Packager选项卡中选中该复选框时，才需要指定 **[!UICONTROL Enable HSM]** 此选项卡中的首选项。 下表介绍了这些首选项：

| 首选项 | 说明 |
|---|---|
| Sun PKCS#11配置文件名 | Sun PKCS#11提供者配置文件的完整路径。 有关此配置文件内容的详细信息，请参阅Sun网站上的Java PKCS#11参考指南。 |
| 分区密码 | 在PKCS#11配置文件中指定的HSM分区的口令。 |
| 许可证服务器证书别名 | 存储在HSM上的Adobe颁发的许可证服务器证书的别名。 此证书用于在打包过程中加密CEK。 在Packager选项卡中指 *定此选项，而不是“License Server Certificate* ”（许可证服务器证书）。 |
| 许可证服务器传输证书别名 | 存储在HSM上的Adobe颁发的服务器传输证书的别名。 此证书用于保护客户端和许可证服务器之间的通信。 在Packager选项卡中指 *定此选项，而不是“License Server Transport Certificate* ”。 |
| Packager凭据别名 | 存储在HSM上的Adobe颁发的打包程序凭据（证书和私钥）的别名。 这用于在打包过程中对元数据进行签名。 在“打包程序”选 *项卡中指定此选项* ，而不是指定Packager Credential。 |
| 许可证服务器凭据别名 | 存储在HSM上的Adobe颁发的许可证服务器凭证（证书和私钥）的别名。 此凭据用于签署策略更新列表。 在“策略更新列表” *选项卡中指定此选项* ，而不是“许可证服务器凭据”。 (此别名可能与“许可证服务器证 *书别名”相同*。) |

