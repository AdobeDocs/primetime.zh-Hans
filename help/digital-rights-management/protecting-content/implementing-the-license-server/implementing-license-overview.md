---
title: 许可证服务器概述
description: 许可证服务器概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# 概述{#license-server-overview}

在向客户端发放许可证之前，必须先部署Adobe Primetime DRM许可证服务器。 许可证服务器使用Primetime DRM SDK执行许多任务。

要实施许可证服务器，请执行以下操作：

* 如果支持用户名/密码身份验证，则处理身份验证请求。
* 处理许可证请求
* 处理获取服务器版本请求 — 所有服务器必须实现对此类型请求的支持。
* 处理域注册请求 — 仅当实现域服务器时才需要。
* 处理域取消注册请求 — 仅当实现域服务器时才需要。
* 进程同步 — 仅当许可证指定同步要求时才需要。

此外，服务器需要提供业务逻辑以对用户进行身份验证，确定用户是否被授权视图内容，并可选地跟踪许可证使用情况。

有关Java API的详细信息，请参阅&#x200B;*Adobe Primetime DRM API参考*。
