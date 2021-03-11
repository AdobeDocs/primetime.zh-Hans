---
title: 更新License Server WAR文件
description: 更新License Server WAR文件
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# 更新License Server WAR文件{#update-the-license-server-war-file}

为了支持通过本地个性化服务器实现个性化的客户端，您必须更新License Server的信任证书根目录以包含新获得的个性化CA凭据。 [!DNL update_license_server]文件夹中包含Python脚本([!DNL addIndivCert.py])。

请执行以下操作以更新许可证服务器：

1. 制作要更新的WAR文件副本(示例：[!DNL flashaccess.war], [!DNL faxsks.war])。
1. 确保已解锁WAR文件并设置其权限，以便修改它们。
1. 运行[!DNL addIndivCert.py] Python脚本以更新License Server WAR文件。

   脚本的输入如下：

   * `cert`:包含个性化CA证书的PKCS12文件
   * `war`:要更新的WAR文件

   输出文件是更新的WAR文件。

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

WAR文件将被修改到位。 如有必要，您可以编辑Python脚本以满足您的特定需求。 执行更新后，可以正常部署WAR文件。
