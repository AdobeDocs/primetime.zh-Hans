---
seo-title: 更新License Server WAR文件
title: 更新License Server WAR文件
uuid: 0cde53d6-185d-4bf2-84fc-0c31d17904a8
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c

---


# 更新License Server WAR文件{#update-the-license-server-war-file}

为了支持通过本地个性化服务器个性化的客户端，您必须更新许可证服务器的信任证书根目录以包含新获取的个性化CA凭证。 文件夹中包 [!DNL addIndivCert.py]含一个Python脚本( [!DNL update_license_server] )。

执行以下操作以更新许可证服务器：

1. 制作要更新的WAR文件副本(示例： [!DNL flashaccess.war], [!DNL faxsks.war])。
1. 确保已解锁WAR文件并设置了其权限，以便修改它们。
1. 运行 [!DNL addIndivCert.py] Python脚本以更新License Server WAR文件。

   脚本的输入如下：

   * `cert`:包含个性化CA证书的PKCS12文件
   * `war`:要更新的WAR文件
   输出文件是更新的WAR文件。

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

WAR文件将被修改到位。 如有必要，您可以编辑Python脚本以满足您的特定需求。 执行更新后，可以正常部署WAR文件。
