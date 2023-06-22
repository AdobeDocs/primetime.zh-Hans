---
title: 使用计算机标识符
description: 使用计算机标识符
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# 使用计算机标识符{#use-machine-identifiers}

所有Adobe Primetime DRM请求（支持FMRMS兼容性的请求除外）都包含有关在个性化过程中颁发给客户端的计算机令牌的信息。 计算机令牌包括计算机ID，它是已在个性化期间分配的标识符。 您可以使用此标识符计算用户从中请求许可证或加入域的计算机数量。

您可以使用标识符，如下所示：

* 此 `getUniqueId()` 方法会返回在个性化过程中分配给设备的字符串。 您可以将字符串存储在数据库中，并按标识符进行搜索。 但是，如果用户重新格式化硬盘驱动器并再次进行个性化，则此标识符会发生变化。 同一台计算机上不同浏览器中的Adobe AIR和AdobeFlash Player之间，此标识符的值也各不相同。
* 如果要更准确地计算计算机数，可以使用 `getBytes()` 以存储整个标识符。 要确定以前是否曾看到过该计算机，请获取用户名的所有标识符并调用 `matches()` 以检查是否匹配。 因为 `matches()` 方法必须用于比较返回的值 `MachineId.getBytes`，此选项仅在要比较的值数量较少时（例如，与特定用户关联的计算机）才切实可行。

