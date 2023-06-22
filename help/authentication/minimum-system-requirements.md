---
title: 最低系统要求
description: 最低系统要求
exl-id: 57b21e2a-abd7-4b4b-85f1-25584a850e40
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# 最低系统要求 {#minimum-system-requirements}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。


## 概述 {#overview}

本文档介绍了在支持的平台上实施Adobe Primetime身份验证集成的当前软件和硬件要求。 下面列出的所有受支持的Web/移动浏览器和操作系统都将受益于绑定到商定SLA的Adobe Primetime身份验证团队的全面支持。

作为Adobe Primetime身份验证团队，我们鼓励使用浏览器和操作系统的最新稳定版本；我们还承认存在当前使用的不兼容/旧版平台和浏览器。 这些过时的设备仍然可以正常工作并且没有问题，但是它们更易出错。

缓解这些过时平台上出现的任何问题的初始方法应该是升级到最新版本；这可以是操作系统版本、浏览器版本或已安装应用程序的版本。

Adobe Primetime身份验证团队将尽最大努力解决这些平台上出现的任何问题。 

Adobe Primetime鼓励我们的客户和合作伙伴考虑升级到最新版本，以便在性能、效率和安全性改进之外，在任何潜在问题上都能从Adobe的完全支持中受益。 


## 浏览器和操作系统要求 {#browser-OS-system-requirements}


| Web/移动浏览器(†) | 支持的版本 |
|---|---|
| Google Chrome | **70** 或更高版本 |
| Mozilla Firefox | **57** 或更高版本 |
| Apple Safari | **14** 或更高版本 |
| Microsoft Edge | **100** 或更高版本 |

(†)Adobe建议不要使用私密或无痕模式。

| 操作系统 | 支持的版本 |
|---|---|
| *Android* | **7.0** (Nougat)或更高版本 |
| *iOS* | **14** 或更高版本 |
| *iPadOS* | **14** 或更高版本 |
| *tvOS* | **14** 或更高版本 |
| *触发操作系统* | **5 (Android 5.1)** 或更高版本 |
| *Mac操作系统* | **10.13** 或更高版本 |
| *Microsoft Windows* | **10** 或更高版本 |




>[!NOTE]
>
>第三方Cookie — 如果禁用了第三方Cookie，Adobe Primetime身份验证权利流可能会失败。  仅当修改浏览器设置时，才会出现此问题。 对于所有受支持的浏览器，Primetime身份验证应以默认设置正常运行。\
 

## 无客户端(REST)实施的设备要求 {#general_clientless_reqs}

 
任何将通过无客户端实施使用Adobe Primetime身份验证服务的设备 **必须能够**：

* 提供唯一的哈希设备ID。 如果设备不提供唯一的经过哈希处理的设备ID，则必须能够保留由Adobe Primetime身份验证提供的唯一ID。 设备应能够在其本地存储中永久保留唯一ID，并在调用Adobe Primetime身份验证API时提供唯一ID作为设备ID。
* 使用HMAC-SHA1算法生成数字签名
* 设置任意HTTP标头
* 使用RESTful Web服务
* 解析XML和JSON数据格式
* 使用HTTPS发送流量
* 处理HTTP错误代码
