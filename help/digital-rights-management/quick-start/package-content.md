---
title: 将加密内容打包
description: 将加密内容打包
copied-description: true
exl-id: e5792917-8172-48b0-8792-7a7e942596c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 将加密内容打包{#package-encrypted-content}

1. 复制 `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` 目录到您的本地文件系统。
1. 在您的本地 `Command Line Tools\` 文件夹，请更新 `flashaccesstools.properties` 使用服务器的文件。

   您必须至少修改以下属性：

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`：许可证服务器证书的路径(通常以 [!DNL .cer]， [!DNL .der] 或 [!DNL .pem])。

   * `encrypt.license.serverurl=[license-server-url]`：您的许可证服务器URL，例如：    `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`.

   * `encrypt.license.servercert=[transport-certificate.cer]`：传输证书的路径(通常以 [!DNL .cer]， [!DNL .der]，或 [!DNL .pem])。

   * `encrypt.sign.certfile=[packager-credentials.pfx]`：Packager证书的路径(以 [!DNL .pfx])。

   * `encrypt.sign.certpass=[password]`：Packager证书的密码。
   >[!NOTE]
   >
   >确保密码不打乱。

1. 创建策略。

   在您的本地 `Command Line Tools\` 文件夹，运行以下命令：

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   此命令创建一个名为的策略文件 [!DNL examplepolicy.pol] 使用匿名许可证服务器身份验证( `-x` 选项)。
1. 将要加密的MP4、FLV或F4V视频文件复制到本地 `Command Line Tools\` 文件夹。
1. 打包您的内容。

   假设您的源视频文件为 [!DNL sample.mp4]. 在您的本地 `Command Line Tools\` 文件夹，运行以下命令：

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >如果要打包HLS、HDS或DASH内容，则必须使用其他打包工具，例如 [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf).

1. 复制加密文件工件（在本例中） [!DNL sample_encrypted.mp4] 和 [!DNL sample_encrypted.mp4.metadata])至 `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`.

此时，您已完成了此过程的打包阶段。

>[!NOTE]
>
>有关打包内容、创建策略等的命令行工具的更多详细信息，请参阅 [Adobe Primetime DRM命令行工具](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md).
