---
description: 'null'
seo-description: 'null'
seo-title: 基于身份的域注册逻辑
title: 基于身份的域注册逻辑
uuid: bc13f7c2-9a20-4f80-b96f-05f7a0fcc343
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 基于身份的域注册逻辑{#identity-based-domain-registration-logic}

## 域注册逻辑 {#section_149C247458954877AF158B4A09A8526B}

该参考实现为基于身份的域注册应用以下逻辑：

1. 确定要分配给指定用户的域名。

   域名( `namequalifier:username`)从身份验证令牌中提取。 如果令牌不可用，则会引发错误。
1. 在表中查找域 `DomainServerInfo` 名。

   如果找不到任何条目，请插入一个条目。 默认值为：

   * `authentication required`
   * `max domain membership=5`
   .

1. 要验证设备是否已注册到域，请执行以下操作：

   1. 查看表 `domainname` 格中的 `UserDomainMembership` 内容：

      1. 对于找到的每个计算机ID，将该ID与请求中的计算机ID进行比较。
      1. 如果这是一台新计算机，请向表中添加一个 `UserDomainMembership` 条目。
      1. 在表中搜索匹配记 `UserDomainRefCount` 录。
      1. 如果此计算机GUID不存在条目，请添加记录。
   1. 如果它是新设备，并且已 `Max Membership` 经到达值，则返回错误。


1. 在表中查找此域的所有域 `DomainKeys` 键：

   1. 如 `DomainServerInfo` 果指示需要滚动密钥，则生成新密钥对，
   1. 将对保存在表 `DomainKeys` 中，其密钥版本高于现有最高密钥的版本。
   1. 在中重 `Key Rollover Required` 置标志 `DomainServerInfo`。

   1. 对于每个域密钥，生成域凭据。

## 域取消注册逻辑 {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

该参考实现为基于身份的域取消注册应用以下逻辑：

1. 确定要分配给此用户的域名。

   域名是从 `namequalifier:username`身份验证令牌中提取的。 如果没有可用的令牌，则会发生返回 `DOM_AUTHENTICATION_REQUIRED (503)` 错误。
1. 在表中查找请求的域 `DomainServerInfo` 名。
1. 在表中查找域 `UserDomainMembership` 名。
1. 将您找到的每个机器ID与请求中的机器ID进行比较。
1. 在表中找到相应的 `UserDomainRefCount` 条目。

   如果找不到匹配的条目，则返回错误。

1. 如果这不是预览请求，请从表中删除该 `UserDomainRefCount` 条目。
1. 如果该表中没有其他计算机条目，请从中删除该条目， `UserDomainMembership` 然后在属性 [!DNL Key Rollover Required] 中设置标 `DomainServerInfo` 志。

每个用户可以注册少量计算机，因此您可以使用完整的计算机ID和方法 `matches()` 对计算机进行计数。 由于用户可以多次注册，通过不同浏览器中的多个AIR应用程序或播放器，服务器需要保持引用计数，以便还可以计算取消注册。

>[!NOTE]
>
>取消注册直到放弃计算机上的所有域令牌后才完成。

