---
seo-title: 网络拓扑概述
title: 网络拓扑概述
uuid: 1558b7fa-dc0d-477c-8f1c-9c6f3718e1b0
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 网络拓扑概述 {#network-topology-overview}

成功部署Adobe Access后，维护环境的安全性非常重要。 本节介绍维护Adobe Access生产服务器的安全性所必需的任务。

使用反 *向代理* ，确保外部和内部用户都可以使用Adobe Access Web应用程序的不同URL集。 此配置比允许用户直接连接到运行Adobe Access的应用程序服务器更安全。 反向代理为运行Adobe Access的应用程序服务器执行所有HTTP请求。 用户只能对反向代理进行网络访问，并且只能尝试反向代理支持的URL连接。

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)

