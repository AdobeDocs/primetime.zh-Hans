---
description: 您可以使用Adobe的machotools工具允许列表您的iOS应用程序。
title: 允许列表iOS应用程序
exl-id: 3af75d9a-3b38-4d3c-9890-513a4abc1809
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 允许列表iOS应用程序 {#allowlist-your-ios-application}

您可以使用Adobe的machotools工具允许列表您的iOS应用程序。

通常，在完成TVSDK应用程序时，您可以使用Adobe Primetime DRM命令行工具来允许列表应用程序。

>[!TIP]
>
>您还可以使用这些工具创建DRM策略并加密内容。

将您的应用程序添加到允许列表可确保只能在视频播放器中播放受保护的内容。 但是，要将iOS应用程序添加到允许列表，您需要完成与Apple的应用程序提交策略配合使用的特殊过程。

在提交iOS应用程序之前，您需要对其进行签名并将其发布到Apple。

>[!NOTE]
>
>Apple会删除开发人员的签名，并使用他们自己的证书重新签署应用程序。

由于重新签名，您在提交到Apple App Store之前生成的允许列表信息不可用。

为了使用此提交策略，Adobe已创建一个 `machotools` 用于对您的iOS应用程序进行指纹识别以创建一个摘要值、对此值进行签名，并将该值注入您的iOS应用程序中的工具。 对iOS应用程序进行指纹识别后，您可以将应用程序提交到Apple App Store。 当用户从App Store运行应用程序时，Primetime DRM会执行应用程序指纹的运行时计算，并使用之前在应用程序中插入的摘要值来确认它。 如果指纹匹配，则确认应用程序允许列出，并允许播放受保护的内容。

Adobe `machotools` 该工具包含在[！DNL]的iOS TVSDK SDK中 [...]/tools/DRM]文件夹。

使用 `machotools`：

1. 生成密钥对。

   要使用OpenSSL等实用程序，请打开命令窗口并输入以下内容：

   ```shell
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. 出现提示时，输入密码以保护私钥。

   密码应至少包含12个字符，字符应混合使用大写和小写ASCII字符和数字。
1. 要使用OpenSSL为您生成强密码，请打开命令窗口并输入以下内容：

   ```shell
   openssl rand -base64 8
   ```

1. 生成证书签名请求(CSR)。

   要使用OpenSSL生成CSR，请打开命令窗口并输入以下内容：

   ```shell
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. 自行签署证书并输入任意持续时间。

   以下示例显示了20年的有效期：

   ```shell
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. 将自签名证书转换为PKCS#12文件：

   ```shell
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   您可以使用自签名证书对您的iOS应用程序进行签名。

1. 更新PFX文件和密码的位置。
1. 在Xcode中构建应用程序之前，请转到  **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** 并将以下命令添加到您的运行脚本中：

   ```shell
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. 执行 [!DNL machotools] 以生成应用程序发布者ID哈希值。

   ```shell
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. 创建新的DRM策略或更新现有策略以包含返回的发布者ID哈希值。
1. 使用 [!DNL AdobePolicyManager.jar]，创建一个新的DRM策略（更新您现有的策略），将返回的发布者ID哈希值、一个可选的应用程序ID以及最小和最大版本属性包含在内 [!DNL flashaccess-tools.properties] 文件。

   ```shell
   java -jar libs/AdobePolicyManager.jar new app_allowlist.pol
   ```

1. 使用新的DRM策略将内容打包，并确认在iOS应用程序中播放允许列出的内容。
