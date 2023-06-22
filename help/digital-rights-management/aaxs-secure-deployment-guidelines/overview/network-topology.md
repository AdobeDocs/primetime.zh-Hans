---
title: 网络拓扑概述
description: 网络拓扑概述
copied-description: true
exl-id: ca5e8701-f8a3-4125-bb60-bfb9efd5c8f3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---

# 网络拓扑概述 {#network-topology-overview}

成功部署Adobe访问后，必须维护环境的安全性。 本节介绍维护Adobe访问生产服务器的安全性所必需的任务。

使用 *反向代理* 确保Adobe访问Web应用程序的URL集对外部和内部用户均可用。 此配置比允许用户直接连接到运行Adobe访问的应用服务器更安全。 反向代理为运行Adobe访问的应用服务器执行所有HTTP请求。 用户仅具有对反向代理的网络访问权限，并且只能尝试反向代理支持的URL连接。

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)
