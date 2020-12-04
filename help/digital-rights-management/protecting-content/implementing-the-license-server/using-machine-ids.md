---
seo-title: 使用机器标识符
title: 使用机器标识符
uuid: 14eee414-62f1-4a9d-84bd-689ca2271d19
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# 使用计算机标识符{#use-machine-identifiers}

所有Adobe PrimetimeDRM请求（支持FMRMS兼容性的请求除外）都包括关于在个性化期间已发送给客户端的机器令牌的信息。 计算机令牌包括计算机ID，该ID是在个性化过程中分配的标识符。 您可以使用此标识符计算用户请求许可证或加入域的计算机数。

您可以按如下方式使用标识符：

* `getUniqueId()`方法返回在个性化过程中已分配给设备的字符串。 可以将字符串存储在数据库中并按标识符进行搜索。 但是，如果用户重新格式化硬盘并再次个性化，则此标识符会更改。 此标识符在同一台计算机上的不同浏览器中的Adobe AIRFlash Player和Adobe之间也具有不同的值。
* 如果要更准确地计算计算机，可使用`getBytes()`存储整个标识符。 要确定以前是否看到过该计算机，请获取用户名的所有标识符并调用`matches()`检查是否有匹配项。 由于`matches()`方法必须用于比较`MachineId.getBytes`返回的值，因此只有在要比较的值较少时，此选项才实用；例如，与特定用户关联的计算机。

