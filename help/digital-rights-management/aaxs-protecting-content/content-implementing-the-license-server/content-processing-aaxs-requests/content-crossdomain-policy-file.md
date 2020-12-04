---
seo-title: 跨域策略文件
title: 跨域策略文件
uuid: fc05aa5e-6fbd-445f-a22a-f795d5a0b3ad
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# 跨域策略文件{#crossdomain-policy-file}

如果许可证服务器托管在视频播放SWF以外的其他域上，则需要一个跨域策略文件(crossdomain.xml)以允许SWF从许可证服务器请求许可证。 跨域策略文件是XML文件，它为服务器提供了一种方法，指示其文档和数据可用于从其他域提供的SWF文件。 允许从许可证服务器的跨域策略文件中指定的域提供的任何SWF文件访问该许可证服务器的数据或资源。

Adobe建议开发人员在部署跨域策略文件时遵循最佳实践，方法是仅允许受信任的域访问许可证服务器并限制对Web服务器上许可证子目录的访问。

有关跨域策略文件的详细信息，请参阅以下位置：

* 网站控制（策略文件）
* 跨域策略文件规范：[https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

