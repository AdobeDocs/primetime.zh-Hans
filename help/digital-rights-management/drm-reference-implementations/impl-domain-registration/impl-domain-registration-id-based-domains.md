---
description: 'null'
seo-description: 'null'
seo-title: 基于身份的域注册逻辑
title: 基于身份的域注册逻辑
uuid: bc13f7c2-9a20-4f80-b96f-05f7a0fcc343
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---


# 基于身份的域注册逻辑{#identity-based-domain-registration-logic}

## 域注册逻辑{#section_149C247458954877AF158B4A09A8526B}

该参考实现将以下逻辑应用于基于身份的域注册：

1. 确定要分配给指定用户的域名。

   域名(`namequalifier:username`)从身份验证令牌中提取。 如果令牌不可用，则引发错误。
1. 在`DomainServerInfo`表中查找域名。

   如果找不到任何条目，请插入一个条目。 默认值为：

   * `authentication required`
   * `max domain membership=5`

   .

1. 要验证设备是否已注册到域：

   1. 查找`UserDomainMembership`表中的`domainname`:

      1. 对于找到的每个计算机ID，将该ID与请求中的计算机ID进行比较。
      1. 如果这是新计算机，请向`UserDomainMembership`表添加一个条目。
      1. 在`UserDomainRefCount`表中搜索匹配记录。
      1. 如果此计算机GUID不存在条目，请添加记录。
   1. 如果它是新设备，并且已达到`Max Membership`值，则返回错误。


1. 在`DomainKeys`表中查找此域的所有域密钥：

   1. 如果`DomainServerInfo`指示需要滚动密钥，则生成新密钥对，
   1. 将对保存在`DomainKeys`表中，密钥版本比现有的最高密钥版本高1。
   1. 重置`DomainServerInfo`中的`Key Rollover Required`标志。

   1. 对于每个域密钥，生成域凭据。

## 域取消注册逻辑{#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

该参考实现对基于身份的域取消注册应用以下逻辑：

1. 确定要分配给此用户的域名。

   域名为`namequalifier:username`，从身份验证令牌中提取。 如果没有可用的令牌，则会发生返回错误`DOM_AUTHENTICATION_REQUIRED (503)`。
1. 在`DomainServerInfo`表中查找请求的域名。
1. 在`UserDomainMembership`表中查找域名。
1. 将您找到的每个计算机ID与请求中的计算机ID进行比较。
1. 在`UserDomainRefCount`表中找到相应的条目。

   如果找不到匹配的条目，则返回错误。

1. 如果这不是预览请求，请从`UserDomainRefCount`表中删除该条目。
1. 如果该表中没有用于计算机的其他条目，则从`UserDomainMembership`中删除该条目，并在`DomainServerInfo`属性中设置[!DNL Key Rollover Required]标志。

每个用户可以注册少量计算机，因此您可以使用完整的计算机ID和`matches()`方法对计算机进行计数。 由于用户可以多次注册，通过不同浏览器中的多个AIR应用程序或播放器，服务器需要保持引用计数，以便还可以计算取消注册。

>[!NOTE]
>
>取消注册直到计算机上的所有域令牌都被放弃后才能完成。

