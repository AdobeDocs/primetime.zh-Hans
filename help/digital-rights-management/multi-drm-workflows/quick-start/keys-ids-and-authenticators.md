---
description: 要实现DRM，您需要特定证书和密钥，包括内容加密密钥或CEK以加密内容，用于保护与ExpressPlay服务器通信的客户身份验证器，以及用于识别存储在密钥管理系统中的内容加密密钥的CEKSID。
seo-description: 要实现DRM，您需要特定证书和密钥，包括内容加密密钥或CEK以加密内容，用于保护与ExpressPlay服务器通信的客户身份验证器，以及用于识别存储在密钥管理系统中的内容加密密钥的CEKSID。
seo-title: 密钥、ID和身份验证器
title: 密钥、ID和身份验证器
uuid: 9e5b1a64-b4e9-442f-ac15-26831aaf585d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 密钥、ID和身份验证器{#keys-ids-and-authenticators}

要实现DRM，您需要特定证书和密钥，包括内容加密密钥或CEK以加密内容，用于保护与ExpressPlay服务器通信的客户身份验证器，以及用于识别存储在密钥管理系统中的内容加密密钥的CEKSID。

您需要这些项目来打包、许可和播放您的受保护内容：

## 内容加密密钥 {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

内容加密密钥(CEK)是用于加密内容的16字节字符串。

**CEK是什么？** - CEK是包装程序用来加密内容的密钥。 这是一个16字节的十六进制编码字符串。

**CEK从何而来？** -您（内容提供者）使用OpenSSL或Notepad++等工具自行创建此密钥。 例如：

```
openssl rand 16 -hex > cek_hex_file
```

或（对于Adobe Offline Packager）:

1. 生成16字节的十六进制编码字符串，如上所示或使用其他工具。 它看起来会像这样：

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. 打开记事本++并粘贴到16字节的十六进制字符串中。
1. 通过Base64编码将此值从十六进制ASCII转换为值，以创建您的值 [!DNL keyfile.bin]。 (此部分包含在 [](../../multi-drm-workflows/quick-start/package-your-content.md)中。)

**同一个钥匙，不同的名字？** -是的，您可能会在其他位置看到由其他名称引用的CEK，例如：

* ** [!DNL [somefile].bin]** - Adobe Offline Packager将CEK称为[!DNL [somefile].bin];例如，* [!DNL Keyfile.bin]* —— 这是Adobe Offline Packager使用的CEK，形式为用于打包内容的计算机上的文件。

   您将随机的CEK十六进制字符串“Base64”保存为文件(例如， [!DNL keyfile.bin])，通常位于下面的 [!DNL creds] 目录中 [!DNL offlinepkgr/]。 在Packager配置文件（例如，如果您要为Widevine DRM打包，则可以调用它）中，您在配置文件中引用CEK，如下所示： [!DNL widevine.xml]

   ```
   <config>  
     <in_path>sample.mp4</in_path>  
     <out_type>dash</out_type>
     <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
     […] 
   </config> 
   ```

* **内容密钥** -在调用( `&contentKey=`)、错误消息、支持票证和其他文档中，您也可以看到称为内容密钥的CEK。

**何时／何处使用它？**

1. 首先，您需要在进行打包的计算机上提供CEK。 您的打包工具使用CEK来加密您的内容。
1. 其次，您需要将CEK存储在某种形式的密钥管理系统(KMS)中，每个CEK都与其自己的内容加密密钥 [相关联](../../multi-drm-workflows/glossary/glossary-cek.md)。 您可以创建自己的KMS，或使用 [ExpressPlay的密钥存储](https://www.expressplay.com/developer/key-storage/)。 这样，您的店面（处理客户授权和许可令牌提供的授权服务器）可以使用密钥ID而不是实际的CEK从KMS中为客户提取许可证令牌（这更加安全）。

## 内容加密密钥存储ID {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

内容加密密钥存储ID(CEKSID)唯一地标识对已加密的视频内容解密的存储密钥。

**CEKSID是什么？** - CEKSID是内容加密密钥(CEK)的唯一标识符。 CEK是解锁受保护内容所必需的；CEKSID是访问CEK的必需SEK，从中存储CEK。 在测试设置时，只要对许可和回放检查使用相同的信息，您就可以在打包时提供随机的CEKSID和CEK。

**它从何而来？** -您（内容提供商）可以自己创建此ID，也可以使用 [ExpressPlay的密钥存储等服务为每个CEK生成CEKSID](https://www.expressplay.com/developer/key-storage/) （并存储这两个CEK）。 此外，您可以使用随机生成的CEKSID，或者使用适合您的业务模型的方案。 例如，您可以使用有意义字符串的CEKSID，而不是随机的十六进制字符串（ID名称可能由主题、日期、时间等组成）

**CEKSID还叫什么？** -它有时称为内 *容ID*。

## 客户身份验证器 {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

客户身份验证器是您在ExpressPlay中设置管理帐户时从ExpressPlay获得的密钥。 身份验证器用于与ExpressPlay服务器通信。

**什么是客户身份验证器？** -两个客户身份验证器组成了这对ID — 一个用于测试，一个用于生产— 在您注册他们的服务时，ExpressPlay会为您注册。 您始终可以在ExpressPlay管理页面上访问它们：
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**我什么时候用这个？** -在对ExpressPlay服务器的所有调用中都包含此功能— 例如，许可服务器、 [ExpressPlay密钥存储](https://www.expressplay.com/developer/key-storage/)，以及其他调用。
