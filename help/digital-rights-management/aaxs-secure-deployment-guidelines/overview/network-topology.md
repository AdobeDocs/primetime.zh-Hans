---
seo-title: 网络拓扑概述
title: 网络拓扑概述
uuid: 1558b7fa-dc0d-477c-8f1c-9c6f3718e1b0
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# 网络拓扑概述{#network-topology-overview}

成功部署Adobe访问后，维护环境的安全性非常重要。 本节介绍维护任务访问生产服务器安全所必需的Adobe。

使用&#x200B;*反向代理*&#x200B;确保外部和内部用户都可以使用Adobe访问Web应用程序的不同URL集。 此配置比允许用户直接连接到运行Adobe访问的应用程序服务器更加安全。 反向代理为运行Adobe访问的应用程序服务器执行所有HTTP请求。 用户只能对反向代理进行网络访问，并且只能尝试反向代理支持的URL连接。

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)

