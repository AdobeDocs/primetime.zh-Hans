---
title: 许可证服务器概述
description: 许可证服务器概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 概述 {#license-server-overview}

您必须先部署Adobe Primetime DRM许可证服务器，然后才能向客户端颁发许可证。 许可证服务器使用Primetime DRM SDK执行多项任务。

要实施许可证服务器，请执行以下操作：

* 如果支持用户名/密码身份验证，则处理身份验证请求。
* 处理许可证请求
* 进程获取服务器版本请求 — 所有服务器都必须对此类型的请求实施支持。
* 处理域注册请求 — 仅在实施域服务器时需要。
* 处理域注销请求 — 仅在实施域服务器时才需要。
* 进程同步 — 仅当许可证指定同步要求时才需要。

此外，服务器需要提供用于验证用户、确定用户是否有权查看内容以及可选地跟踪许可证使用的业务逻辑。

请参阅 *Adobe Primetime DRM API参考* 以了解有关Java API的详细信息。
