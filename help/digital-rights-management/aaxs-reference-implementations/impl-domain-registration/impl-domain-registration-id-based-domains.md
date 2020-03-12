---
seo-title: 基于身份的域
title: 基于身份的域
uuid: 34cad19b-1adb-4e0c-ac59-50632f6988f7
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 基于身份的域 {#identity-based-domains}

在此用例中，每个经过身份验证的用户都有自己的域，并且允许一定数量的设备加入该域。 要将此类域与引用实现一起使用，需要创建一个指定域注册的策略。 指定您的服务器的主机和域服务器URL的端口，并指定用户名／密码身份验证为必需条件。

该参考实现实现了域注册的以下逻辑：

1. 确定要分配给此用户的域名。 该域名将从身份验证令 `namequalifier:username`牌中提取**。 如果没有身份验证令牌，则返回错误DOM_AUTHENTICATION_REQUIRED(503)。
1. 在表中查找域 `DomainServerInfo` 名。 如果找不到某个条目，请在表中插入一个条目（默认值是身份验证要求，最大域成员资格为5）。
1. 检查设备是否已向域注册：

   1. 在表中查找域 `UserDomainMembership` 名。 对于找到的每个计算机ID，请与请求中的计算机ID进行比较。 如果这是一台新计算机，请向表中添加一个 `UserDomainMembership` 条目。 然后，在表中查找匹配的 `UserDomainRefCount` 记录。 如果此计算机GUID不存在条目，请添加记录。

   1. 如果它是新设备并且已达到最大成员资格，则返回错误DOM_LIMIT_REACHED(502)。

1. 在DomainKeys表中查找此域的所有域密钥。

   1. 如果 `DomainServerInfo` 指示需要滚动密钥，请生成新密钥对，将其保存在表中（密钥版本1比现有的最高密钥高），并在中重置“需要滚动密钥”标志 `DomainKeys``DomainServerInfo`。

   1. 对于每个域密钥，生成域凭据。

该参考实现实现了域取消注册的以下逻辑：

1. 确定要分配给此用户的域名。 域名将从身份验 *证令牌中提取namequalifier:username* 。 如果没有身份验证令牌，则返回错误DOM_AUTHENTICATION_REQUIRED(503)。
1. 在表中查找请求的域 `DomainServerInfo` 名。
1. 在表中查找域 `UserDomainMembership` 名。 对于找到的每个计算机ID，请与请求中的计算机ID进行比较。 在表中查找相应的 `UserDomainRefCount` 条目。 如果找不到匹配条目，则返回错误DEREG_DENIED(401)。

1. 如果这不是预览请求，则从表中删除该 `UserDomainRefCount` 条目。 如果该表中没有其他计算机条目，则从中删除该条目， `UserDomainMembership` 并在中设置“Key Rollover Required”标志 `DomainServerInfo`。

在这种情况下，允许每个用户注册少量的机器，这样我们就可以使用完整的机器ID和方法来准确 `matches()` 地对机器进行计数。 但是，由于用户可以在这台机器上多次注册（通过不同浏览器中的多个AIR应用程序或播放器），服务器还需要保持参考计数，以便准确计算取消注册。 取消注册不能被视为完成，除非机器上的所有域令牌都被放弃。
