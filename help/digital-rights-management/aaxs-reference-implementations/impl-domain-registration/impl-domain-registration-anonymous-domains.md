---
seo-title: 匿名域
title: 匿名域
uuid: ee29ae4d-65b2-48de-b441-18c8cf55de32
translation-type: tm+mt
source-git-commit: 4f196bbd079edeb1a423afee6b4b7e249d380f40
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# 匿名域 {#anonymous-domains}

在此用例中，大量设备属于单个域，可能不需要身份验证。 要在引用实现中使用此类域，请创建指定需要域注册的策略。 将域服务器URL指定为并 `https:// host:port/flashaccess/domainserver/domainname/` 指定匿名身份验证。

该参考实现实现了域注册的以下逻辑：

1. 解析请求URL中的域名。
1. 在表中查找域 `DomainServerInfo` 名。 如果找不到某个条目，请在表中插入一个条目(默认值：身份验证不是必需的，并且不最大限制成员资格)。
1. 如果请求的域需要身份验证，请确保请求中包含有效的身份验证令牌，并与身份验证命名空间匹配（如果在数据库中指定）。

   1. 如果需要身份验证但未提供有效的身份验证令牌，则返回错误 `DOM_AUTHENTICATION_REQUIRED (503)`。

1. 检查设备是否已注册到域：

   1. 在表中查找域 `DomainMembership` 名。 对于找到的每个计算机GUID，请与请求中的计算机GUID进行比较。 如果这是新计算机，则向表中添加一个 `DomainMembership` 条目。

   1. 如果它是新设备并且已达到最大成员资格，则返回错误 `DOM_LIMIT_REACHED (502)`。

1. 在表中查找此域的所有域 `DomainKeys` 键。

   1. 如 `DomainServerInfo` 果指示需要滚动密钥，生成新密钥对，将其保存在表中(密钥版本 `DomainKeys` 高于现有最高密钥的版本1)，并在中重置 `Key Rollover Required` 标志 `DomainServerInfo`。

   1. 对于每个域密钥，生成域凭据。

该参考实现实现了域取消注册的以下逻辑：

1. 解析请求URL中的域名。
1. 在表中查找请求的域 `DomainServerInfo` 名。
1. 如果请求的域需要身份验证，请确保请求中包含有效的身份验证令牌，并与身份验证命名空间匹配（如果在数据库中指定）。
1. 在表中查找域名和计算机 `DomainMembership` GUID。 如果找不到匹配的条目，则返回错误 `DEREG_DENIED (401)`。

1. 如果这不是预览请求，则从中删除该条目 `DomainMembership` 并在中 `Key Rollover Required` 设置标志 `DomainServerInfo`。

在此用例中，由于大量计算机可以加入域，因此无法完全匹配计算机ID。 而是使用在个性化过程中分配给计算机的随机计算机GUID。
