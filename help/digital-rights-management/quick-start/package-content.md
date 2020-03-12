---
seo-title: 打包加密内容
title: 打包加密内容
uuid: 1e271167-107d-41df-8a7c-3075cb3acc0c
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 打包加密内容{#package-encrypted-content}

1. 将目录复 `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` 制到本地文件系统。
1. 在您的本地文 `Command Line Tools\` 件夹中，更新文 `flashaccesstools.properties` 件以便与您的服务器一起使用。

   您必须至少修改以下属性：

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`:您的许可证服务器证书的路径(通常以或 [!DNL .cer]结尾 [!DNL .der] ) [!DNL .pem]。

   * `encrypt.license.serverurl=[license-server-url]`:您的许可证服务器URL，例如：   `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`.

   * `encrypt.license.servercert=[transport-certificate.cer]`:传输证书的路径(通常以、 [!DNL .cer]或 [!DNL .der]结尾 [!DNL .pem])。

   * `encrypt.sign.certfile=[packager-credentials.pfx]`:Packager证书的路径(此路径以 [!DNL .pfx]结尾)。

   * `encrypt.sign.certpass=[password]`:Packager证书的口令。
   >[!NOTE]
   >
   >请确保不要扰乱密码。

1. 创建策略。

   在您的本地文 `Command Line Tools\` 件夹中，运行以下命令：

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   此命令创建一个名为的策略文 [!DNL examplepolicy.pol] 件，该文件使用匿名的许可证服务器身份验证( `-x` 选项)。
1. 将要加密的MP4、FLV或F4V视频文件复制到本地文件夹 `Command Line Tools\` 中。
1. 打包您的内容。

   假设源视频文件是 [!DNL sample.mp4]。 在您的本地文 `Command Line Tools\` 件夹中，运行以下命令：

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >如果要打包HLS、HDS或DASH内容，则必须使用其他打包工具，如 [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)。

1. 将加密的文件伪像(在本例中为 [!DNL sample_encrypted.mp4] 和)复 [!DNL sample_encrypted.mp4.metadata]制到 `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`。

此时，您已完成了该过程的打包阶段。

>[!NOTE]
>
>有关用于打包内容、创建策略等的命令行工具的更多详细信息，请参 [阅Adobe Primetime DRM命令行工具](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md)。
