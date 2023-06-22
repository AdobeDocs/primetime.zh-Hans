---
title: 基于身份的域
description: 基于身份的域
copied-description: true
exl-id: de7b6c8a-5227-4679-933a-3278921903d7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# 基于身份的域 {#identity-based-domains}

在此使用案例中，每个经过身份验证的用户都有自己的域，并且允许一定数量的设备加入该域。 若要将此类型的域用于引用实施，需要创建一个策略，指定域注册。 为域服务器URL指定服务器的主机和端口，并指定需要用户名/密码身份验证。

参考实施为域注册实现了以下逻辑：

1. 确定要分配给此用户的域名。 域名将为* `namequalifier:username`*从身份验证令牌提取。 如果没有身份验证令牌，则返回错误DOM_AUTHENTICATION_REQUIRED (503)。
1. 在中查找域名 `DomainServerInfo` 表格。 如果未找到某个条目，请在表中插入一个条目（默认值为需要身份验证，最大域成员资格=5）。
1. 检查设备是否已向域注册：

   1. 在中查找域名 `UserDomainMembership` 表格。 对于找到的每个计算机ID，与请求中的计算机ID进行比较。 如果这是一台新计算机，请将一个条目添加到 `UserDomainMembership` 表格。 接下来，在中查找匹配的记录 `UserDomainRefCount` 表格。 如果此计算机GUID不存在条目，请添加记录。

   1. 如果这是新设备，并且已达到最大成员资格，则会返回错误DOM_LIMIT_ACCEEDED (502)。

1. 在DomainKeys表中查找此域的所有域密钥。

   1. 如果 `DomainServerInfo` 表示需要翻转密钥，生成新的密钥对，并将其保存在 `DomainKeys` 表（键的版本比现有的最高键高1），并在表中重置“需要键变换”标志 `DomainServerInfo`.

   1. 对于每个域密钥，生成域凭据。

参考实现，为域注销实现了以下逻辑：

1. 确定要分配给此用户的域名。 域名将为 *namequalifier：username* 从身份验证令牌提取。 如果没有身份验证令牌，则返回错误DOM_AUTHENTICATION_REQUIRED (503)。
1. 在中查找请求的域名 `DomainServerInfo` 表格。
1. 在中查找域名 `UserDomainMembership` 表格。 对于找到的每个计算机ID，与请求中的计算机ID进行比较。 在中查找对应的条目 `UserDomainRefCount` 表格。 如果找不到匹配的条目，则返回错误DEREG_DENIED (401)。

1. 如果这不是预览请求，请从删除条目 `UserDomainRefCount` 表格。 如果该计算机表中没有其他条目，则从中删除该条目 `UserDomainMembership` 并在中设置“需要密钥变换”标记 `DomainServerInfo`.

在此使用案例中，允许每个用户注册少量计算机，因此我们可以使用完整的计算机ID和 `matches()` 精确计数机器的方法。 但是，由于用户可在此计算机上多次注册(通过多个AIR应用程序或不同浏览器中的播放器)，服务器还需要维护引用计数，以便准确计算注销次数。 除非移交计算机上的所有域令牌，否则不能将注销视为完成。
