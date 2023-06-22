---
title: HSM首选项
description: HSM首选项
copied-description: true
exl-id: 323f839b-fbd8-492c-a210-7651e92c7513
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# HSM首选项 {#hsm-preferences}

仅当满足以下条件时，才需要指定此选项卡中的首选项 **[!UICONTROL Enable HSM]** 复选框在Packager选项卡中处于选中状态。 下表描述了这些首选项：

| 首选项 | 描述 |
|---|---|
| Sun PKCS#11配置文件名 | Sun PKCS#11提供程序配置文件的完整路径。 有关此配置文件内容的详细信息，请参阅Sun网站上的《Java PKCS#11参考指南》。 |
| 分区密码 | PKCS#11配置文件中指定的HSM分区的密码。 |
| 许可证服务器证书别名 | Adobe颁发的许可证服务器证书的别名存储在HSM上。 此证书用于在打包期间加密CEK。 指定此值，而不是 *许可证服务器证书* 在Packager选项卡中。 |
| 许可证服务器传输证书别名 | 存储在HSM上的Adobe颁发的服务器传输证书的别名。 此证书用于保护客户端和许可证服务器之间的通信。 指定此值，而不是 *许可证服务器传输证书* 在Packager选项卡中。 |
| Packager凭据别名 | 存储在HSM上的Adobe颁发的打包程序凭据（证书和私钥）的别名。 这用于在打包期间对元数据进行签名。 指定此值，而不是 *Packager凭据* 在Packager选项卡中。 |
| 许可证服务器凭据别名 | Adobe颁发的许可证服务器凭据（证书和私钥）的别名存储在HSM上。 此凭据用于签署策略更新列表。 指定此值，而不是 *许可证服务器凭据* 在“策略更新列表”选项卡中。 (此别名可能与 *许可证服务器证书别名*.) |
