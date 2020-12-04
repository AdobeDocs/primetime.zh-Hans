---
description: 您可以使用Adobe的machotools工具允许列表iOS应用程序。
seo-description: 您可以使用Adobe的machotools工具允许列表iOS应用程序。
seo-title: 允许列表iOS应用程序
title: 允许列表iOS应用程序
uuid: bc558f5f-d4e6-4c1c-81eb-f8bd61c63016
translation-type: tm+mt
source-git-commit: eb9f0a2f6d2118b953c711dfdc0402d1d923b016
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# 允许列表iOS应用程序{#allowlist-your-ios-application}

您可以使用Adobe的machotools工具允许列表iOS应用程序。

通常，在您完成TVSDK应用程序时，可以使用Adobe PrimetimeDRM命令行工具来允许列表您的应用程序。

>[!TIP]
>
>您还可以使用这些工具创建DRM策略并加密内容。

允许列出您的应用程序可确保受保护的内容只能在视频播放器中播放。 但是，允许列出iOS应用程序需要您完成与Apple的应用程序提交策略配合的特殊过程。

在提交iOS应用程序之前，您需要对它进行签名，然后将其发布到Apple。

>[!NOTE]
>
>Apple会删除您的开发人员的签名，并使用他们自己的证书重新签署应用程序。

由于重新签名，您提交到Apple App Store之前生成的允许列表信息不可用。

要使用此提交策略，Adobe已创建`machotools`工具，该工具将指纹指示您的iOS应用程序以创建摘要值、签署此值并将此值注入您的iOS应用程序。 在您为iOS应用程序建立指纹后，您可以将该应用程序提交到Apple App Store。 当用户从App Store运行您的应用程序时，Primetime DRM会对应用程序指纹进行运行时计算，并使用之前在应用程序中注入的摘要值确认它。 如果指纹匹配，则确认该应用程序允许列出，并允许播放受保护的内容。

Adobe`machotools`工具包含在[!DNL [的iOS TVSDK SDK中……]/tools/DRM]文件夹。

要使用`machotools`:

1. 生成密钥对。

   要使用OpenSSL等实用程序，请打开命令窗口并输入以下内容：

   ```shell
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. 出现提示时，输入密码以保护私钥。

   密码至少应包含12个字符，且字符应包含大小写ASCII字符和数字的混合。
1. 要使用OpenSSL为您生成强口令，请打开命令窗口并输入以下内容：

   ```shell
   openssl rand -base64 8
   ```

1. 生成证书签名请求(CSR)。

   要使用OpenSSL生成CSR，请打开命令窗口并输入以下内容：

   ```shell
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. 自行签署证书并输入任何持续时间。

   以下示例给出了20年的过期时间：

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
1. 在Xcode中构建应用程序之前，请转至&#x200B;**[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]**，并将以下命令添加到运行脚本：

   ```shell
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. 执行[!DNL machotools]以生成应用程序Publisher ID哈希值。

   ```shell
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. 创建新的DRM策略或更新现有策略以包含返回的发布者ID哈希值。
1. 使用[!DNL AdobePolicyManager.jar]创建新的DRM策略（更新现有策略），以在包含的[!DNL flashaccess-tools.properties]文件中包含返回的发布者ID哈希值、可选的应用程序ID以及最小和最大版本属性。

   ```shell
   java -jar libs/AdobePolicyManager.jar new app_allowlist.pol
   ```

1. 使用新的DRM策略打包内容并确认在iOS应用程序中播放允许列出的内容。
