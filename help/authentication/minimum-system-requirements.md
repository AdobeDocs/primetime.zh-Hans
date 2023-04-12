---
title: 最低系统要求
description: 最低系统要求
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# 最低系统要求 {#minimum-system-requirements}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。


## 概述 {#overview}

本文档介绍在受支持的平台上实施Adobe Primetime身份验证集成的当前软件和硬件要求。 下面列出的所有受支持的Web/移动浏览器和操作系统都将受益于Adobe Primetime身份验证团队的完全支持，该团队将遵守商定的SLA。

作为Adobe Primetime身份验证团队，我们鼓励使用浏览器和操作系统的最新稳定版本；我们还确认当前使用的不兼容/旧版平台和浏览器的存在。 这些过时的设备仍可以正常运行，但更容易出错。

缓解这些过时平台上出现的任何问题的初始方法应该升级到最新版本；这可以是操作系统版本、浏览器版本或已安装应用程序的版本。

这些平台上出现的任何问题都将由Adobe Primetime身份验证团队尽力解决。 

Adobe Primetime鼓励我们的客户和合作伙伴考虑升级到最新版本，以便除性能、效率和安全性改进外，在任何潜在问题上都能从Adobe的全面支持中受益。 


## 浏览器和操作系统要求 {#browser-OS-system-requirements}


| Web/移动设备浏览器(†) | 支持的版本 |
|---|---|
| Google Chrome | **70** 或更高版本 |
| Mozilla Firefox | **57** 或更高版本 |
| Apple Safari | **14** 或更高版本 |
| Microsoft Edge | **100** 或更高版本 |

(†)Adobe建议不要使用私密或隐身模式。

| 操作系统 | 支持的版本 |
|---|---|
| *Android* | **7.0** （努加特）或更高版本 |
| *iOS* | **14** 或更高版本 |
| *iPadOS* | **14** 或更高版本 |
| *tvOS* | **14** 或更高版本 |
| *Fire OS* | **5(Android 5.1)** 或更高版本 |
| *Mac OS* | **10.13** 或更高版本 |
| *Microsoft Windows* | **10** 或更高版本 |




>[!NOTE]
>
>第三方Cookie — 禁用第三方Cookie时，Adobe Primetime身份验证授权流可能会失败。  仅当浏览器设置被修改时，才会播放此问题。 对于所有受支持的浏览器，Primetime身份验证应使用默认设置正常运行。\
 

## 无客户端(REST)实施的设备要求 {#general_clientless_reqs}

 
通过无客户端实施使用Adobe Primetime身份验证服务的任何设备 **必须能够**:

* 提供一个唯一且经过哈希处理的设备ID。 如果设备未提供经过哈希处理的唯一设备ID，则必须能够保留由Adobe Primetime身份验证提供的唯一ID。 设备应该能够将唯一ID永久保留在其本地存储中，并在调用Adobe Primetime身份验证API时将唯一ID作为设备ID提供。
* 使用HMAC-SHA1算法生成数字签名
* 设置任意HTTP标头
* 使用RESTful Web服务
* 解析XML和JSON数据格式
* 使用HTTPS发送流量
* 处理HTTP错误代码
