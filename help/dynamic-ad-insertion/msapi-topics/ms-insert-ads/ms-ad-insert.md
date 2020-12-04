---
description: 所有广告插入请求都使用相同的URL结构和相同的基本查询参数。 附加的查询参数使清单服务器能够处理各种客户端和情况。
seo-description: 所有广告插入请求都使用相同的URL结构和相同的基本查询参数。 附加的查询参数使清单服务器能够处理各种客户端和情况。
seo-title: 广告插入请求
title: 广告插入请求
uuid: e42b3228-bff7-4202-86ed-7f631f3016ae
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# 广告插入请求{#requests-for-ad-insertion}

所有广告插入请求都使用相同的URL结构和相同的基本查询参数。 附加的查询参数使清单服务器能够处理各种客户端和情况。

| 参数 | 说明 |
|--- |--- |
| u | 资产ID是来自Adobe Primetime广告决策元数据的ad_request_id的MD5哈希。 由Adobe技术客户经理提供。 |
| z | 需要提供给Auditude的资产的区域ID。 由Adobe技术客户经理提供。 |
| `__sid__` | 清单服务器将用于生成会话ID的唯一ID。 |

>[!NOTE]
>
>`__sid__`参数周围有多次下划线字符。

清单服务器为单个客户机或客户机组维护会话，以确保不同客户机的API交互序列保持独立。 客户端在引导URL中发送给清单服务器的`__sid__`在其环境中应是唯一的。 清单服务器使用它构建全局唯一ID，它将其返回给客户端。

其余的查询参数与不同的客户端和情况有关。