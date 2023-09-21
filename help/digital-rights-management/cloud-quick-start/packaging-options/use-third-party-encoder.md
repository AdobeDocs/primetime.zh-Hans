---
title: 使用第三方编码器
description: 使用第三方编码器
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 使用第三方编码器{#use-a-third-party-encoder}

有些客户可能已经使用硬件或软件视频编码器(或Adobe Media Server)准备内容。 如果是这种情况，任何当前可创建受Primetime DRM保护内容的产品都可以使用与Primetime Cloud DRM保护工具包相同的配置设置来为Primetime Cloud DRM打包内容。 所需信息可从套件中包含的任何现有配置文件中获取： [!DNL config_hls.xml] 或 [!DNL config_hds.xml].

相关配置项目包括：

* 许可证服务器URL
* 密钥服务器URL
* 许可证服务器证书
* 传输证书
