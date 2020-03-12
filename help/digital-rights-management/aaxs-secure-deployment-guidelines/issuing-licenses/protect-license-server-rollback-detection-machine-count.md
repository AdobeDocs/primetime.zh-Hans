---
seo-title: 颁发许可证时的计算机计数
title: 颁发许可证时的计算机计数
uuid: d57f8b0b-0363-4b26-bd71-76f4abe5b68f
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 颁发许可证时的计算机计数{#machine-count-when-issuing-licenses}

如果业务规则要求跟踪用户的计算机数，则许可证服务器或域服务器必须存储与用户关联的计算机ID。 跟踪机器ID的最可靠方法是将该方法返回的值存 `MachineId.getBytes()` 储在数据库中。 当出现新请求时，请使用将请求中的计算机ID与已知的计算机ID进行比较 `MachineId.matches()`。

`MachineId.matches()` 执行ID比较以确定它们是否代表同一台计算机。 只有少量机器ID可与之进行比较时，此比较才可行。 例如，如果允许用户在其域内使用五台计算机，则可以在数据库中搜索与用户用户名关联的计算机ID，并获取一小组要进行比较的数据。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>此比较对于允许匿名访问的部署来说不现实。 但是，在 `MachineId.getUniqueID()` 这种情况下，如果用户从Flash和Adobe AIR®运行时访问内容，则此ID将不相同，如果用户重新设置硬盘的格式，则此ID将不会继续存在。

要进一步了解 `MachineToken.getMachineId()`和 `MachineId.matches()`，请参 *阅Adobe Access API参考*。
