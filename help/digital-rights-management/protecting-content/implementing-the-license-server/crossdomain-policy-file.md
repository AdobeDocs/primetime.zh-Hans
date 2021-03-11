---
title: 跨域DRM策略文件
description: 跨域DRM策略文件
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# 跨域DRM策略文件{#crossdomain-drm-policy-file}

如果许可证服务器托管在与视频播放SWF不同的域上，则需要跨域DRM策略文件([!DNL crossdomain.xml])，以使SWF能够从许可证服务器请求许可证。 跨域DRM策略文件由XML文件表示，该文件使服务器能够指示其数据和文档对从其他域提供的SWF文件可用。 允许从许可证服务器的跨域DRM策略文件中指定的域提供的任何SWF文件访问该许可证服务器中的数据或资源。

Adobe建议开发人员在部署跨域策略文件时遵循最佳做法，方法是仅允许受信任的域访问许可证服务器并限制对Web服务器上许可证子目录的访问。

有关跨域DRM策略文件的详细信息，请参阅以下位置：

* 网站控制（DRM策略文件）
* 跨域DRM策略文件规范：[https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

