---
title: 匿名域逻辑
description: 匿名域逻辑
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# 匿名域逻辑{#anonymous-domain-logic}

## 域注册逻辑{#section_C91DCD49D7D44570AF98C2D7B8A283F9}

引用实现对匿名域注册应用以下逻辑：

1. 解析请求URL中的域名。
1. 在`DomainServerInfo`表中查找域名。
1. 如果找不到条目，请在表中插入条目。

   默认值为：

   * `authentication is not required`
   * `no membership maximum`

   如果请求的域需要身份验证，请确保请求中包含有效的身份验证令牌。 如果在数据库中指定了身份验证命名空间，则令牌必须与指定的身份验证命名空间匹配。
1. 如果需要身份验证，但无有效的身份验证令牌可用，则返回错误`DOM_AUTHENTICATION_REQUIRED (503)`。
1. 检查设备是否已注册到域：

   1. 在`DomainMembership`表中查找域名。
   1. 将您找到的计算机GUID与请求中的计算机GUID进行比较。
   1. 如果这是新计算机，请在`DomainMembership`表中添加一个条目。
   1. 如果它是新设备，且已达到`Max Membership`值，则返回错误`DOM_LIMIT_REACHED (502)`。

1. 在`DomainKeys`表中查找此域的所有域密钥：

   1. 如果`DomainServerInfo`指示需要滚动密钥，则生成新密钥对。
   1. 在`DomainKeys`表中保存密钥对，密钥版本比现有最高密钥高一个数。
   1. 重置`DomainServerInfo`中的`Key Rollover Required`标志。

   1. 对于每个域密钥，生成域凭据。

## 域取消注册逻辑{#section_C968BBFCBFAB4510A903D169F38C9FCE}

引用实现对匿名域取消注册应用以下逻辑：

1. 解析请求URL中的域名。
1. 在`DomainServerInfo`表中查找请求的域名。
1. 如果请求的域需要身份验证，请确保请求中包含有效的身份验证令牌。

   令牌还必须与在数据库中指定的身份验证命名空间匹配。
1. 在`DomainMembership`表中查找域名和计算机GUID。

   如果找不到匹配的条目，则返回错误`DEREG_DENIED (401)`。

1. 如果这不是预览请求，请从`DomainMembership`中删除该条目，在`DomainServerInfo`中设置`Key Rollover Required`标志。

由于许多计算机可能加入域，因此您不能简单地与计算机ID匹配。 而是应用在个性化过程中分配给计算机的随机计算机GUID。
