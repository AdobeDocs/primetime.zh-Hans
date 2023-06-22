---
title: 匿名域
description: 匿名域
copied-description: true
exl-id: a9358582-ad25-4016-94d2-cd82b4c00573
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# 匿名域 {#anonymous-domains}

在此使用案例中，大量设备属于单个域，并且可能不需要身份验证。 若要将此类型的域用于引用实施，请创建策略，指定域注册是必需的。 将域服务器URL指定为 `https:// host:port/flashaccess/domainserver/domainname/` 和指定匿名身份验证。

参考实施为域注册实现了以下逻辑：

1. 从请求URL中解析域名。
1. 在中查找域名 `DomainServerInfo` 表格。 如果未找到某个条目，则在表中插入一个条目（默认值：无需验证，并且没有成员资格上限）。
1. 如果请求的域需要身份验证，请确保请求中包含有效的身份验证令牌，并匹配身份验证命名空间（如果在数据库中指定）。

   1. 如果需要身份验证，但未提供有效的身份验证令牌，则返回错误 `DOM_AUTHENTICATION_REQUIRED (503)`.

1. 检查设备是否已向域注册：

   1. 在中查找域名 `DomainMembership` 表格。 对于找到的每个计算机GUID，请与请求中的计算机GUID进行比较。 如果这是一台新计算机，请将一个条目添加到 `DomainMembership` 表格。

   1. 如果这是新设备，并且已达到最大成员资格，则会返回错误 `DOM_LIMIT_REACHED (502)`.

1. 在中查找此域的所有域密钥 `DomainKeys` 表格。

   1. 如果 `DomainServerInfo` 指示需要滚动的键，生成新的键对，并将其保存在 `DomainKeys` 表（键版本比最高的现有键版本高一），并重置 `Key Rollover Required` 标记位置 `DomainServerInfo`.

   1. 对于每个域密钥，生成域凭据。

参考实施为域注销实现了以下逻辑：

1. 从请求URL中解析域名。
1. 在中查找请求的域名 `DomainServerInfo` 表格。
1. 如果请求的域需要身份验证，请确保请求中包含有效的身份验证令牌，并匹配身份验证命名空间（如果在数据库中指定）。
1. 在中查找域名和计算机GUID `DomainMembership` 表格。 如果找不到匹配的条目，则返回错误 `DEREG_DENIED (401)`.

1. 如果这不是预览请求，请从删除条目 `DomainMembership` 并设置 `Key Rollover Required` 标记位置 `DomainServerInfo`.

在此使用案例中，由于大量计算机可以加入域，因此不可能完全匹配计算机ID。 而是使用在个性化期间分配给计算机的随机计算机GUID。
