---
title: 更新许可证服务器WAR文件
description: 更新许可证服务器WAR文件
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 更新许可证服务器WAR文件{#update-the-license-server-war-file}

为了支持通过本地个性化服务器进行个性化的客户端，您必须更新许可证服务器的信任证书根以包含新获得的个性化CA凭据。 Python脚本( [!DNL addIndivCert.py])包含在中 [!DNL update_license_server] 文件夹。

执行以下操作以更新许可证服务器：

1. 制作要更新的WAR文件的副本(示例： [!DNL flashaccess.war]， [!DNL faxsks.war])。
1. 确保已解锁WAR文件并已设置其权限以便对其进行修改。
1. 运行 [!DNL addIndivCert.py] 用于更新许可证服务器WAR文件的Python脚本。

   脚本的输入值如下：

   * `cert`：包含个性化CA证书的PKCS12文件
   * `war`：要更新的WAR文件

   输出文件是更新的WAR文件。

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

将就地修改WAR文件。 如有必要，您可以编辑Python脚本以满足您的特定需求。 执行更新后，可以正常部署WAR文件。
