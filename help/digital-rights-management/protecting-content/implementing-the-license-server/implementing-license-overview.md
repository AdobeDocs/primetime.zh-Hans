---
title: 许可证服务器概述
description: 许可证服务器概述
copied-description: true
exl-id: 101d9f63-b9b9-4281-a069-8c66427b34cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 概述 {#license-server-overview}

必须先部署Adobe Primetime DRM许可证服务器，然后才能向客户端颁发许可证。 许可证服务器使用Primetime DRM SDK执行多项任务。

要实施许可证服务器，请执行以下操作：

* 如果支持用户名/密码身份验证，则处理身份验证请求。
* 处理许可证请求
* 进程获取服务器版本请求 — 所有服务器都必须对此类型的请求实施支持。
* 处理域注册请求 — 仅在实施域服务器时需要。
* 处理域注销请求 — 仅在实施域服务器时需要。
* 进程同步 — 仅当许可证指定同步要求时才需要。

此外，服务器需要提供业务逻辑来验证用户，确定用户是否有权查看内容，以及选择性地跟踪许可证使用情况。

参见 *Adobe Primetime DRM API参考* 以了解有关Java API的详细信息。
