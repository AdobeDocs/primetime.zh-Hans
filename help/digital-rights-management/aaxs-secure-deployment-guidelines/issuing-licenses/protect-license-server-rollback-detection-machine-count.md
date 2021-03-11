---
title: 颁发许可证时的计算机计数
description: 颁发许可证时的计算机计数
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# 颁发许可证时的计算机计数{#machine-count-when-issuing-licenses}

如果业务规则要求跟踪用户的计算机数，则许可证服务器或域服务器必须存储与用户关联的计算机ID。 跟踪机器ID的最可靠方法是将`MachineId.getBytes()`方法返回的值存储在数据库中。 当有新请求出现时，请使用`MachineId.matches()`将请求中的计算机ID与已知的计算机ID进行比较。

`MachineId.matches()` 执行ID比较，以确定它们是否代表同一台计算机。只有与之比较的机器ID数较少时，此比较才可用。 例如，如果允许用户在其域中使用五台计算机，则可以搜索数据库以查找与用户用户名关联的计算机ID，并获取一小组要进行比较的数据。

>[!NOTE]
>
>此比较对于允许匿名访问的部署来说不实用。 在这种情况下，可以使用`MachineId.getUniqueID()`，但是，如果用户从Flash和Adobe AIR®运行时访问内容，则此ID将不相同，如果用户重新格式化其硬盘，则此ID将不会继续存在。

要进一步了解`MachineToken.getMachineId()`和`MachineId.matches()`，请参阅&#x200B;*Adobe访问API参考*。
