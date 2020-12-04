---
seo-title: 使用机器标识符
title: 使用机器标识符
uuid: 2832c158-fade-4bbf-ae89-f95ce9dfc369
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# 使用计算机标识符{#using-machine-identifiers}

所有Adobe访问请求（支持FMRMS兼容性的请求除外）都包含有关在个性化过程中发布给客户端的计算机令牌的信息。 计算机令牌包含计算机ID，即在个性化过程中分配的标识符。 使用此标识符可计算用户请求许可证或加入域的计算机数。

使用标识符有两种方法。 `getUniqueId()`方法返回在个性化期间分配给设备的字符串。 可以将字符串存储在数据库中并按标识符进行搜索。 但是，如果用户重新格式化硬盘并重新个性化，则此标识符将发生更改。 此标识符在同一台计算机上的不同浏览器中的Adobe® AIR®和Adobe®Flash®播放器之间也具有不同的值。

要更准确地计算计算机，您可以使用`getBytes()`存储整个标识符。 要确定以前是否看到过该计算机，请获取用户名的所有标识符并调用`matches()`检查是否有匹配项。 因为必须使用`matches()`方法来比较`MachineId.getBytes`返回的值，所以只有当要比较的值数不多时（例如，与特定用户关联的计算机），此选项才实用。
