---
title: 基于身份的域
description: 基于身份的域
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# 基于身份的域{#identity-based-domains}

在此用例中，每个经过身份验证的用户都有自己的域，并允许某些设备加入域。 要将此类型的域与引用实现一起使用，请创建一个策略，指定域注册。 指定域服务器URL的服务器主机和端口，并指定用户名/密码身份验证为必需。

该引用实现实现了域注册的以下逻辑：

1. 确定要分配给此用户的域名。 域名将从身份验证令牌中提取* `namequalifier:username`*。 如果没有身份验证令牌，则返回错误DOM_AUTHENTICATION_REQUIRED(503)。
1. 查找`DomainServerInfo`表中的域名。 如果找不到某个条目，请在表中插入一个条目（默认值是身份验证要求，最大域成员资格=5）。
1. 检查设备是否已向域注册：

   1. 查找`UserDomainMembership`表中的域名。 对于找到的每个计算机ID，请与请求中的计算机ID进行比较。 如果这是新计算机，请向`UserDomainMembership`表添加一个条目。 然后，在`UserDomainRefCount`表中查找匹配记录。 如果此计算机GUID不存在条目，请添加记录。

   1. 如果它是新设备，并且已达到最大成员资格，则返回错误DOM_LIMIT_REACHED(502)。

1. 在DomainKeys表中查找此域的所有域密钥。

   1. 如果`DomainServerInfo`指示需要滚动密钥，则生成新密钥对，将其保存在`DomainKeys`表中（密钥版本比现有最高密钥版本高1），并重置`DomainServerInfo`中的“需要滚动密钥”标志。

   1. 对于每个域密钥，生成域凭据。

该参考实现实现了域取消注册的以下逻辑：

1. 确定要分配给此用户的域名。 域名将从身份验证令牌中提取为&#x200B;*namequalifier:username*。 如果没有身份验证令牌，则返回错误DOM_AUTHENTICATION_REQUIRED(503)。
1. 在`DomainServerInfo`表中查找请求的域名。
1. 查找`UserDomainMembership`表中的域名。 对于找到的每个计算机ID，请与请求中的计算机ID进行比较。 在`UserDomainRefCount`表中查找相应的条目。 如果找不到匹配项，则返回错误DEREG_DENIED(401)。

1. 如果这不是预览请求，请从`UserDomainRefCount`表中删除该条目。 如果该表中没有计算机的其他条目，请从`UserDomainMembership`中删除该条目，并在`DomainServerInfo`中设置“需要密钥变换”标志。

在此用例中，允许每个用户注册少量计算机，因此我们可以使用完整的计算机ID和`matches()`方法来准确计算计算机。 但是，由于用户可以在此计算机上多次注册（通过不同浏览器中的多个AIR应用程序或播放器），服务器还需要保持引用计数，以便准确计数取消注册。 在放弃计算机上的所有域令牌之前，取消注册不能被视为完成。
