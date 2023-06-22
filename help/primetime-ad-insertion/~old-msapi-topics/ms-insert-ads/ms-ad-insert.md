---
description: 所有广告插入请求都使用相同的URL结构和相同的基本查询参数。 通过其他查询参数，清单服务器可以处理各种客户端和情况。
title: 广告插入请求
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# 广告插入请求 {#requests-for-ad-insertion}

所有广告插入请求都使用相同的URL结构和相同的基本查询参数。 通过其他查询参数，清单服务器可以处理各种客户端和情况。

| 参数 | 描述 |
|--- |--- |
| u | 资源ID是Adobe Primetime ad decisioning元数据中ad_request_id的MD5哈希值。 由您的Adobe技术客户经理提供。 |
| z | 需要提供给Auditude的资产的区域ID。 由您的Adobe技术客户经理提供。 |
| `__sid__` | 清单服务器将用于生成会话ID的唯一ID。 |

>[!NOTE]
>
>此 `__sid__` 参数被双下划线字符包围。

清单服务器为单个客户端或客户端组维护会话，以确保不同客户端的API交互序列保持独立。 此 `__sid__` 客户端在引导URL中发送到清单服务器的内容在其环境中应是唯一的。 清单服务器使用它构造一个全局唯一ID，并将其返回给客户端。

其余查询参数适用于不同的客户端和情况。