---
title: 跨域策略文件
description: 跨域策略文件
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 跨域策略文件 {#crossdomain-policy-file}

如果许可证服务器托管在不同于视频播放SWF的域上，则需要跨域策略文件(crossdomain.xml)以允许SWF从许可证服务器请求许可证。 跨域策略文件是一种XML文件，它为服务器提供了一种方法，用于指示其数据和文档可用于SWF从其他域提供的文件。 从许可证服务器的跨域SWF文件中指定的域提供的任何策略文件都允许从该许可证服务器访问数据或资产。

Adobe建议开发人员在部署跨域策略文件时遵循最佳实践，仅允许受信任域访问许可证服务器，并限制对Web服务器上许可证子目录的访问。

有关跨域策略文件的详细信息，请参阅以下位置：

* 网站控件（策略文件）
* 跨域策略文件规范： [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
