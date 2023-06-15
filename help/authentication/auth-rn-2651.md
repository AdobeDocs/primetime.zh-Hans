---
title: Adobe Pass Authentication 2.65.1发行说明
description: Adobe Pass Authentication 2.65.1发行说明
source-git-commit: c8259e3268556c20630fff92aa90b0f7f9c12617
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Adobe Pass Authentication 2.65.1发行说明 {#authn-2651-rn}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

本页介绍了此版本的新增功能、更改和已知问题：

## 服务器端和Web客户端 {#server-side-web-clients-2651}

* [内部版本号](#build-number-2651)
* [发行版概述](#release-overview-2651)

### 内部版本号 {#build-number-2651}

Adobe Pass身份验证： adobe-pass-**2.65.1**
发行日期： **06/20/2023 - 06/22/2023**

### 发行版概述 {#release-overview-2651}

此版本添加了以下内容：

从本版本开始，我们将引入在所有API中添加速率限制规则的技术支持，以保护整个生态系统免受错误使用。

初始目标是监视应用程序行为以建立适当的限制值，在此版本中不会应用任何限制。 如果特定应用程序生成的流量超过某些限制，我们将与每位客户合作来验证实施。

在我们验证从所有客户的应用程序生成的流量后，今年晚些时候将应用速率限制规则。
