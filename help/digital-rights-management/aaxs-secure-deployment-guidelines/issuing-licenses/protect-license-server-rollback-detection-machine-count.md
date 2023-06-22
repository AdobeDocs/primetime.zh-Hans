---
title: 颁发许可证时的计算机计数
description: 颁发许可证时的计算机计数
copied-description: true
exl-id: de052e98-8ae3-4e12-8f77-787293edda39
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 颁发许可证时的计算机计数{#machine-count-when-issuing-licenses}

如果业务规则要求跟踪用户的计算机数，则License Server或Domain Server必须存储与该用户关联的计算机ID。 跟踪计算机ID的最可靠方法是存储 `MachineId.getBytes()` 数据库中的方法。 传入新请求时，使用将请求中的计算机ID与已知的计算机ID进行比较 `MachineId.matches()`.

`MachineId.matches()` 执行ID比较以确定它们是否代表同一计算机。 只有在要比较的机器ID数量较少时，这种比较才切实可行。 例如，如果允许用户在其域内使用五台计算机，则您可以在数据库中搜索与用户用户名关联的计算机ID，并获取一小部分数据以进行比较。

>[!NOTE]
>
>这种比较对于允许匿名访问的部署并不实际。 在这种情况下 `MachineId.getUniqueID()` 但是，如果用户同时从Flash和Adobe AIR®运行时访问内容，则此ID将不同，并且如果用户重新格式化其硬盘，此ID将无法存留。

要了解有关 `MachineToken.getMachineId()`和 `MachineId.matches()`，请参见 *Adobe访问API参考*.
