---
seo-title: 使用第三方编码器
title: 使用第三方编码器
uuid: 8649303c-b8e6-4c02-a8ad-5734af850bfe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用第三方编码器{#use-a-third-party-encoder}

某些客户可能已使用硬件或软件视频编码器（或Adobe Media Server）准备了内容准备管道。 如果出现这种情况，任何当前可创建受DRM保护的内容的产品都可以使用与Primetime Cloud DRM保护套件相同的配置设置来打包Primetime Cloud DRM的内容。 可从套件中包含的任一现有配置文件获取所需的信息：或 [!DNL config_hls.xml] 者 [!DNL config_hds.xml]。

相关配置项包括：

* 许可证服务器URL
* 密钥服务器URL
* 许可证服务器证书
* 传输证书

