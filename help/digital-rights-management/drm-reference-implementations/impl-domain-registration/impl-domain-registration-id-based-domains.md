---
title: 基于身份的域注册逻辑
description: 基于身份的域注册逻辑
copied-description: true
exl-id: 6e391fce-00b4-45cf-b785-3b0ec734a11e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 基于身份的域注册逻辑{#identity-based-domain-registration-logic}

## 域注册逻辑 {#section_149C247458954877AF158B4A09A8526B}

参考实施将以下逻辑应用于基于身份的域注册：

1. 确定要分配给指定用户的域名。

   域名( `namequalifier:username`)从身份验证令牌中提取。 如果令牌不可用，则会引发错误。
1. 在中查找域名 `DomainServerInfo` 表格。

   如果未找到任何条目，则插入一个条目。 默认值为：

   * `authentication required`
   * `max domain membership=5`

   .

1. 验证设备是否已向域注册：

   1. 查找 `domainname` 在 `UserDomainMembership` 表：

      1. 对于找到的每个计算机ID，将该ID与请求中的计算机ID进行比较。
      1. 如果这是一台新计算机，请将一个条目添加到 `UserDomainMembership` 表格。
      1. 在中搜索匹配记录 `UserDomainRefCount` 表格。
      1. 如果此计算机GUID不存在条目，请添加记录。
   1. 如果是新设备，并且 `Max Membership` 已达到值，返回错误。


1. 在中查找此域的所有域密钥 `DomainKeys` 表：

   1. 如果 `DomainServerInfo` 表示密钥需要滚动，生成新的密钥对，
   1. 将配对保存在 `DomainKeys` 表，其键版本比现有的最高键高1。
   1. 重置 `Key Rollover Required` 标记位置 `DomainServerInfo`.

   1. 对于每个域密钥，生成域凭据。

## 域注销逻辑 {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

参考实施将以下逻辑应用于基于身份的域注销：

1. 确定要分配给此用户的域名。

   域名是 `namequalifier:username`，从身份验证令牌中提取。 如果没有可用的令牌，则返回错误 `DOM_AUTHENTICATION_REQUIRED (503)` 发生。
1. 在中查找请求的域名 `DomainServerInfo` 表格。
1. 在中查找域名 `UserDomainMembership` 表格。
1. 将找到的每个计算机ID与请求中的计算机ID进行比较。
1. 在中找到相应的条目 `UserDomainRefCount` 表格。

   如果找不到匹配的条目，则返回错误。

1. 如果这不是预览请求，请从以下位置删除该条目： `UserDomainRefCount` 表格。
1. 如果该表中没有其他计算机条目，则从中删除该条目 `UserDomainMembership` 并设置 [!DNL Key Rollover Required] 中的标志 `DomainServerInfo` 属性。

每个用户可以注册少量计算机，因此您可以使用完整的计算机ID和 `matches()` 计数计算机的方法。 由于用户可以通过多个AIR应用程序或不同浏览器中的播放器多次注册，因此服务器需要保持引用计数，以便注销也可以计数。

>[!NOTE]
>
>在移交计算机上的所有域令牌之前，注销不会完成。
