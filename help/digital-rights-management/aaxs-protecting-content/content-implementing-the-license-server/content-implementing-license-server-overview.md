---
seo-title: 概述
title: 概述
uuid: f4ae10ca-6e2a-4313-80a0-4c7377dba000
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# 概述{#overview}

要向客户颁发许可证，您必须部署Adobe访问许可证服务器。 许可证服务器使用Adobe® Access™ SDK执行以下任务:

* 如果支持用户名／密码身份验证，则处理身份验证请求。
* 处理许可证请求
* 处理获取服务器版本请求——所有服务器都必须实现对此类请求的支持。
* 处理域注册请求——仅当实现域服务器时才需要。
* 处理域取消注册请求——仅当实现域服务器时才需要。
* 进程同步——仅当许可证指定同步要求时才需要。

此外，服务器需要提供业务逻辑以对用户进行身份验证，确定用户是否有权对内容进行视图，并有选择地跟踪许可证使用情况。

有关本章中讨论的Java API的详细信息，请参阅&#x200B;*Adobe访问API参考*。
