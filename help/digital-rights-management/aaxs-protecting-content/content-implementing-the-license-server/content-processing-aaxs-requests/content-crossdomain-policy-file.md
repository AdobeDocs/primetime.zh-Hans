---
title: 跨域策略文件
description: 跨域策略文件
copied-description: true
exl-id: dbe16692-cdf7-4a91-9303-8afc2d487112
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 跨域策略文件 {#crossdomain-policy-file}

如果许可证服务器托管在不同于视频播放SWF的域上，则需要一个跨域策略文件(crossdomain.xml)，以允许SWF从许可证服务器请求许可证。 跨域策略文件是一个XML文件，它提供一种方法，使服务器能够指示其数据和文档可用于SWF从其他域提供的文件。 允许从许可证服务器的跨域SWF文件中指定的域提供的任何策略文件访问该许可证服务器中的数据或资产。

Adobe建议开发人员在部署跨域策略文件时遵循最佳实践，仅允许受信任的域访问许可证服务器，并限制对Web服务器上许可证子目录的访问。

有关跨域策略文件的详细信息，请参阅以下位置：

* 网站控件（策略文件）
* 跨域策略文件规范： [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
