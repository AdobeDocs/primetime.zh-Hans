---
title: 使用第三方编码器
description: 使用第三方编码器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 使用第三方编码器{#use-a-third-party-encoder}

某些客户可能已经使用硬件或软件视频编码器(或Adobe Medium服务器)准备了内容准备管道。 如果出现这种情况，任何当前可创建Primetime DRM保护内容的产品都可以使用与Primetime Cloud DRM保护工具包相同的配置设置打包Primetime Cloud DRM的内容。 可从套件中包含的任何现有配置文件获取所需信息：[!DNL config_hls.xml]或[!DNL config_hds.xml]。

相关配置项为：

* 许可证服务器URL
* 密钥服务器URL
* 许可证服务器证书
* 传输证书

