---
description: Adobe Primetime DRM的任何使用都包括在工作流的不同时间点执行的两个关键步骤。 每个资产必须完成一次内容准备，并导致创建受保护的内容。 每个希望观看受保护资产的消费者都要多次获取内容。
title: 内容准备
exl-id: 6ec8e5a1-3cf4-498b-9cbb-760c525fb9c7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 内容准备{#content-preparation}

Adobe Primetime DRM的任何使用都包括在工作流的不同时间点执行的两个关键步骤。 每个资产必须完成一次内容准备，并导致创建受保护的内容。 每个希望观看受保护资产的消费者都要多次获取内容。

在使内容可用于分发之前，必须首先以视频格式对内容进行编码，创建一个或多个指定内容使用规则的策略，并使用Adobe Primetime DRM SDK打包内容。

编码、打包和分发内容的步骤如下：

1. 使用Adobe或第三方提供的编码工具对所需视频格式的内容进行编码。
1. 创建指定使用者可以查看其内容的使用规则的策略。

   策略是规则和限制的容器，用于确定消费者查看受保护内容的方式、时间和位置。

   打包程序至少需要一个策略，其中至少有一个使用规则。 当License Server生成许可证时，您可以覆盖使用规则，并添加其他使用规则。

1. 打包内容并指定要应用的策略。

   Primetime DRM SDK使用内容加密密钥(CEK)加密内容，并将一个或多个策略绑定到内容。 结果是一个*受保护的内容文件*只能由从相应的许可证服务器获得许可证的消费者播放。

   在打包期间，将使用CEK对内容进行加密。 使用许可证服务器公钥对CEK进行加密，并将其随策略一起包含在Primetime DRM元数据中。 Primetime DRM元数据使用Packager私钥进行签名，元数据包含在受保护内容中。

1. 使受保护的内容可用于分发给消费者。

   受保护的内容通常使用内容分发网络(CDN)分发。 CDN可以使用客户端运行时支持的任何机制，例如Flash Media Server、用于多比特率流的AdobeHTTP Dynamic Streaming或用于渐进式下载的HTTP Web服务器。
