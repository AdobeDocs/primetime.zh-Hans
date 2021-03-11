---
title: 匿名域
description: 匿名域
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# 匿名域{#anonymous-domains}

在此用例中，大量设备属于单个域，可能不需要身份验证。 要将此类型的域与引用实现一起使用，请创建指定需要域注册的策略。 将域服务器URL指定为`https:// host:port/flashaccess/domainserver/domainname/`并指定匿名身份验证。

该引用实现实现了域注册的以下逻辑：

1. 解析请求URL中的域名。
1. 查找`DomainServerInfo`表中的域名。 如果找不到某个条目，请在表中插入一个条目(默认值：身份验证不是必需的，并且没有最大的成员资格)。
1. 如果请求的域需要身份验证，请确保请求中包含有效的身份验证令牌，并与身份验证命名空间匹配（如果在数据库中指定）。

   1. 如果需要身份验证但未提供有效的身份验证令牌，则返回错误`DOM_AUTHENTICATION_REQUIRED (503)`。

1. 检查设备是否已向域注册：

   1. 查找`DomainMembership`表中的域名。 对于找到的每台计算机GUID，请与请求中的计算机GUID进行比较。 如果这是新计算机，请向`DomainMembership`表添加一个条目。

   1. 如果它是新设备，并且已达到最大成员资格，则返回错误`DOM_LIMIT_REACHED (502)`。

1. 在`DomainKeys`表中查找此域的所有域密钥。

   1. 如果`DomainServerInfo`指示需要滚动密钥，则生成新密钥对，将其保存在`DomainKeys`表中（密钥版本比现有最高密钥版本高1），并在`DomainServerInfo`中重置`Key Rollover Required`标志。

   1. 对于每个域密钥，生成域凭据。

该引用实现实现了域取消注册的以下逻辑：

1. 解析请求URL中的域名。
1. 在`DomainServerInfo`表中查找请求的域名。
1. 如果请求的域需要身份验证，请确保请求中包含有效的身份验证令牌，并与身份验证命名空间匹配（如果在数据库中指定）。
1. 查找`DomainMembership`表中的域名和计算机GUID。 如果找不到匹配项，则返回错误`DEREG_DENIED (401)`。

1. 如果这不是预览请求，则从`DomainMembership`中删除该条目，并在`DomainServerInfo`中设置`Key Rollover Required`标志。

在此用例中，由于大量计算机可以加入域，因此无法完全匹配计算机ID。 而是使用在个性化过程中分配给计算机的随机计算机GUID。
