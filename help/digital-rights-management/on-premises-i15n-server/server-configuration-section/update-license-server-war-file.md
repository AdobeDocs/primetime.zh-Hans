---
title: 更新许可证服务器WAR文件
description: 更新许可证服务器WAR文件
copied-description: true
exl-id: a70d04e2-24a4-4848-9e9b-97467f2c1749
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 更新许可证服务器WAR文件{#update-the-license-server-war-file}

为了支持通过本地个性化服务器进行个性化的客户端，您必须更新许可证服务器的信任证书根目录，以包含新获得的个性化CA凭据。 Python脚本( [!DNL addIndivCert.py])包含在中 [!DNL update_license_server] 文件夹。

执行以下操作以更新许可证服务器：

1. 复制要更新的WAR文件(示例： [!DNL flashaccess.war]， [!DNL faxsks.war])。
1. 确保WAR文件已解锁，并已设置其权限以便可以修改。
1. 运行 [!DNL addIndivCert.py] 用于更新许可证服务器WAR文件的Python脚本。

   脚本输入值如下：

   * `cert`：包含个性化CA证书的PKCS12文件
   * `war`：要更新的WAR文件

   输出文件是一个更新的WAR文件。

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

将就地修改WAR文件。 如有必要，您可以编辑Python脚本以满足您的特定需求。 执行更新后，可以正常部署WAR文件。
