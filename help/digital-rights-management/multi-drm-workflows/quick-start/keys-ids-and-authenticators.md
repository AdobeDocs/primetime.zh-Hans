---
description: 要实施DRM，您需要特定的证书和密钥，包括用于加密内容的内容加密密钥或CEK、用于保护与ExpressPlay服务器通信的客户验证器，以及用于识别存储在密钥管理系统中的内容加密密钥的CEKSID。
title: 密钥、ID和身份验证程序
exl-id: b769192d-92ad-4b93-84dd-80b182fc6c43
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---

# 密钥、ID和身份验证程序{#keys-ids-and-authenticators}

要实施DRM，您需要特定的证书和密钥，包括用于加密内容的内容加密密钥或CEK、用于保护与ExpressPlay服务器通信的客户验证器，以及用于识别存储在密钥管理系统中的内容加密密钥的CEKSID。

您需要以下项目来打包、许可和播放受保护的内容：

## 内容加密密钥 {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

内容加密密钥(CEK)是用于加密内容的16字节字符串。

**什么是CEK？** - CEK是打包程序用于加密内容的密钥。 是一个16字节的十六进制编码字符串。

**CEK从何而来？**  — 您（内容提供商）自行使用OpenSSL或Notepad++等工具创建此密钥。 例如：

```
openssl rand 16 -hex > cek_hex_file
```

或(对于AdobeOffline Packager)：

1. 如上所述或使用其他工具生成16字节十六进制编码字符串。 它看上去将类似于此：

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. 打开Notepad++并粘贴到16字节十六进制字符串中。
1. 通过Base64将此值从十六进制ASCII转换 — 对该值进行编码以创建您的 [!DNL keyfile.bin]. (此部分涵盖在 [](../../multi-drm-workflows/quick-start/package-your-content.md).)

**相同的键值，不同的名称？**  — 是，您可能会看到在其他位置有其他名称引用的CEK，例如：

* ** [！DNL [somefile].bin]** -Adobe脱机打包程序将CEK称为[！DNL [somefile].bin]；例如，* [!DNL Keyfile.bin]* — 这是您的CEK，由Adobe脱机打包程序使用，采用文件形式，位于您用于打包内容的计算机上。

   将“Base64”作为随机CEK十六进制字符串，并将其另存为文件(例如， [!DNL keyfile.bin])，通常位于 [!DNL creds] 目录下 [!DNL offlinepkgr/]. 在Packager配置文件中(例如，您可以将其称为 [!DNL widevine.xml] 如果您是为Widevine DRM打包)，请在配置文件中参阅CEK，如下所示：

   ```
   <config>  
     <in_path>sample.mp4</in_path>  
     <out_type>dash</out_type>
     <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
     […] 
   </config> 
   ```

* **内容密钥**  — 您还可能会看到在调用中称为内容键的CEK( `&contentKey=`)、错误消息中、支持票证中和其他文档中。

**何时/在何处使用它？**

1. 首先，您需要在打包时使用的计算机上提供CEK。 打包工具使用CEK对内容进行加密。
1. 其次，您需要以某种形式的密钥管理系统(KMS)来存储CEK，每个CEK都与其自身相关联 [内容加密密钥](../../multi-drm-workflows/glossary/glossary-cek.md). 您可以创建自己的KMS，也可以使用 [ExpressPlay的密钥存储](https://www.expressplay.com/developer/key-storage/). 这样，您的店面（负责处理客户权利和许可证令牌配置的授权服务器）就可以使用密钥ID而不是实际的CEK从KMS中提取客户的许可证令牌（这样更加安全）。

## 内容加密密钥存储标识 {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

内容加密密钥存储ID (CEKSID)唯一标识用于解密加密的视频内容的存储密钥。

**什么是CEKSID？** - CEKSID是内容加密密钥(CEK)的唯一标识符。 解锁受保护内容需要CEK；要从存储内容的CEK访问，需要CEKSID。 在测试设置时，您可以在打包时提供随机的CEKSID和CEK，但前提是使用相同的信息进行许可和播放检查。

**它是从哪里来的？**  — 您（内容提供商）可以自行创建此ID，也可以使用之类的服务 [ExpressPlay的密钥存储](https://www.expressplay.com/developer/key-storage/) 为每个CEK生成CEKSID（并存储两者）。 此外，您可以使用随机生成的CEKSID，或采用适合您的业务模型的方案。 例如，您可以使用是有意义的字符串（而不是随机的十六进制字符串）的CEKSID（ID名称可能包含主题、日期、时间等）

**CEKSID还叫什么来着？**  — 有时称为 *内容Id*.

## 客户验证器 {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

客户验证器是您在那里设置管理员帐户时从ExpressPlay获得的密钥。 验证器用于与ExpressPlay服务器通信。

**什么是客户身份验证器？**  — 两个客户验证者构成了ExpressPlay在您注册其服务时为您注册的ID对（一个用于测试，一个用于生产）。 您始终可以在ExpressPlay管理页面上使用它们：
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**我何时使用它？**  — 将此包括在对ExpressPlay服务器(例如，许可证服务器、 [ExpressPlay密钥存储](https://www.expressplay.com/developer/key-storage/)和其他调用。
