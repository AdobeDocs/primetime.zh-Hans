---
seo-title: 使用机器标识符
title: 使用机器标识符
uuid: 2832c158-fade-4bbf-ae89-f95ce9dfc369
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用机器标识符{#using-machine-identifiers}

所有Adobe Access请求（支持FMRMS兼容性的请求除外）都包含在个性化过程中发布给客户端的计算机令牌的相关信息。 机器令牌包含一个机器ID，一个在个性化过程中分配的标识符。 使用此标识符可计算用户从中请求许可证或加入域的计算机数。

有两种使用标识符的方法。 该方 `getUniqueId()` 法返回在个性化期间分配给设备的字符串。 可以将字符串存储在数据库中并按标识符进行搜索。 但是，如果用户重新设置硬盘的格式并再次个性化，则此标识符将会更改。 该标识符在同一台计算机上的不同浏览器中的Adobe® AIR®和Adobe® Flash® Player之间也具有不同的值。

要更精确地计算机，您可以使用 `getBytes()` 存储整个标识符。 要确定计算机之前是否已被看到，请获取用户名的所有标识符并调用以 `matches()` 检查是否匹配。 由于必 `matches()``MachineId.getBytes`须使用该方法来比较返回的值，因此，只有当要比较的值数较少时（例如，与特定用户关联的计算机），此选项才可用。
