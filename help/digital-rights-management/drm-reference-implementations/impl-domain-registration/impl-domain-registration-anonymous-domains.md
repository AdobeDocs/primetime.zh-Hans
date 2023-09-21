---
title: 匿名域逻辑
description: 匿名域逻辑
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 匿名域逻辑{#anonymous-domain-logic}

## 域注册逻辑 {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

引用实现将以下逻辑应用于匿名域注册：

1. 从请求URL中解析域名。
1. 在中查找域名 `DomainServerInfo` 表格。
1. 如果找不到某个条目，请在表中插入一个条目。

   默认值为：

   * `authentication is not required`
   * `no membership maximum`

   如果请求的域需要身份验证，请确保请求中包含有效的身份验证令牌。 如果在数据库中指定了身份验证命名空间，则令牌必须与指定的身份验证命名空间匹配。
1. 如果需要进行身份验证，但有效的身份验证令牌不可用，则返回错误 `DOM_AUTHENTICATION_REQUIRED (503)`.
1. 检查设备是否已在域中注册：

   1. 在中查找域名 `DomainMembership` 表格。
   1. 将您找到的计算机GUID与请求中的计算机GUID进行比较。
   1. 如果这是一台新计算机，请在 `DomainMembership` 表格。
   1. 如果是新设备并且 `Max Membership` 已达到值，返回错误 `DOM_LIMIT_REACHED (502)`.

1. 在中查找此域的所有域密钥 `DomainKeys` 表：

   1. 如果 `DomainServerInfo` 指示需要翻转密钥，生成新的密钥对。
   1. 将密钥对保存在 `DomainKeys` 表，其键版本比现有的最高键高一个数字。
   1. 重置 `Key Rollover Required` 标记位置 `DomainServerInfo`.

   1. 对于每个域密钥，生成域凭据。

## 域注销逻辑 {#section_C968BBFCBFAB4510A903D169F38C9FCE}

引用实现将以下逻辑应用于匿名域注销：

1. 从请求URL中解析域名。
1. 在中查找请求的域名 `DomainServerInfo` 表格。
1. 如果请求的域需要身份验证，请确保请求中包含有效的身份验证令牌。

   令牌还必须与数据库中指定的身份验证命名空间匹配。
1. 在中查找域名和计算机GUID `DomainMembership` 表格。

   如果找不到匹配的条目，则返回错误 `DEREG_DENIED (401)`.

1. 如果这不是预览请求，请从以下位置删除条目 `DomainMembership`、和 `DomainServerInfo`，设置 `Key Rollover Required` 标志。

由于大量计算机可能加入域，因此不能简单地匹配计算机ID。 而是应用个性化期间分配给计算机的随机计算机GUID。
