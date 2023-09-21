---
title: 使用计算机标识符
description: 使用计算机标识符
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 使用计算机标识符{#using-machine-identifiers}

所有Adobe访问请求（支持FMRMS兼容性的请求除外）都包含有关在个性化期间颁发给客户端的计算机令牌的信息。 计算机令牌包含计算机ID，这是一种在个性化期间分配的标识符。 使用此标识符可计算用户从中请求许可证或加入域的计算机的数量。

标识符有两种使用方式。 此 `getUniqueId()` 方法会返回在个性化期间分配给设备的字符串。 您可以将字符串存储在数据库中，并按标识符进行搜索。 但是，如果用户重新格式化硬盘驱动器并再次对其进行个性化，则此标识符将发生变化。 此标识符在Adobe® AIR®与同一计算机上不同浏览器中的Adobe®Flash®播放器之间也具有不同的值。

要更准确地计数计算机，您可以使用 `getBytes()` 用于存储整个标识符。 要确定以前是否看到过该计算机，请获取用户名的所有标识符并调用 `matches()` 以检查是否匹配。 因为 `matches()` 方法必须用于比较返回的值 `MachineId.getBytes`，此选项仅当要比较的值数量较少时（例如，与特定用户关联的计算机）才具有实用性。
