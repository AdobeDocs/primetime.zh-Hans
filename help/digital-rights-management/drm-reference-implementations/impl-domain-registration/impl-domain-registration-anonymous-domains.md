---
description: 'null'
seo-description: 'null'
seo-title: 匿名域逻辑
title: 匿名域逻辑
uuid: bd0e8e51-27dc-4ccf-b285-a80c2ab9e260
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 匿名域逻辑{#anonymous-domain-logic}

## 域注册逻辑 {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

引用实现为匿名域注册应用以下逻辑：

1. 解析请求URL中的域名。
1. 在表中查找域 `DomainServerInfo` 名。
1. 如果找不到某个条目，请在表中插入一个条目。

   默认值为：

   * `authentication is not required`
   * `no membership maximum`
   如果请求的域需要身份验证，请确保请求中包含有效的身份验证令牌。 如果在数据库中指定了身份验证命名空间，则令牌必须与指定的身份验证命名空间匹配。
1. 如果需要身份验证，但有效的身份验证令牌不可用，则返回错误 `DOM_AUTHENTICATION_REQUIRED (503)`。
1. 检查设备是否已向域注册：

   1. 在表中查找域 `DomainMembership` 名。
   1. 将您找到的计算机GUID与请求中的计算机GUID进行比较。
   1. 如果这是一台新计算机，请在表中添加一个 `DomainMembership` 条目。
   1. 如果它是新设备且已 `Max Membership` 达到值，则返回错误 `DOM_LIMIT_REACHED (502)`。

1. 在表中查找此域的所有域 `DomainKeys` 键：

   1. 如 `DomainServerInfo` 果指示需要滚动键，则生成新的键对。
   1. 将密钥对保存在 `DomainKeys` 表中，其中密钥版本比现有的最高密钥版本高一个数字。
   1. 在中重 `Key Rollover Required` 置标志 `DomainServerInfo`。

   1. 对于每个域密钥，生成域凭据。

## 域取消注册逻辑 {#section_C968BBFCBFAB4510A903D169F38C9FCE}

引用实现对匿名域取消注册应用以下逻辑：

1. 解析请求URL中的域名。
1. 在表中查找请求的域 `DomainServerInfo` 名。
1. 如果请求的域需要身份验证，请确保请求中包含有效的身份验证令牌。

   该令牌还必须与在数据库中指定的身份验证命名空间匹配。
1. 在表中查找域名和计算机GUID。 `DomainMembership`

   如果找不到匹配的条目，则返回错误 `DEREG_DENIED (401)`。

1. 如果这不是预览请求，则从中删除该条目， `DomainMembership`并在中 `DomainServerInfo`设置标 `Key Rollover Required` 志。

由于许多计算机可能加入域，因此您不能简单地与计算机ID匹配。 而是应用在个性化过程中分配给计算机的随机计算机GUID。
