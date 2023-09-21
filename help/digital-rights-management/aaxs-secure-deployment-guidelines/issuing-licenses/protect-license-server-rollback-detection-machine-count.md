---
title: 颁发许可证时的计算机计数
description: 颁发许可证时的计算机计数
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 颁发许可证时的计算机计数{#machine-count-when-issuing-licenses}

如果业务规则要求跟踪用户的计算机数，则许可证服务器或域服务器必须存储与该用户关联的计算机ID。 跟踪计算机ID的最可靠方法是存储 `MachineId.getBytes()` 数据库中的方法。 传入新请求时，使用将请求中的计算机ID与已知的计算机ID进行比较 `MachineId.matches()`.

`MachineId.matches()` 执行ID比较，以确定它们是否代表同一台计算机。 仅当要比较的机器ID数量较少时，这种比较才具有实用性。 例如，如果用户在其域中允许使用五台计算机，则您可以在数据库中搜索与用户用户名关联的计算机ID，并获取一小部分数据以进行比较。

>[!NOTE]
>
>这种比较对于允许匿名访问的部署不实用。 在这种情况下 `MachineId.getUniqueID()` 但是，如果用户从Flash和Adobe AIR运行时访问内容，则此ID将不同，®且如果用户重新格式化其硬盘，此ID将无法存留。

要了解有关 `MachineToken.getMachineId()`和 `MachineId.matches()`，请参见 *Adobe访问API参考*.
