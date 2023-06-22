---
description: 如果业务规则要求跟踪用户的计算机数，则License Server或Domain Server必须存储与该用户关联的计算机ID。
title: 颁发许可证时的计算机计数
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# 颁发许可证时的计算机计数 {#machine-count-when-issuing-licenses}

如果业务规则要求跟踪用户的计算机数，则License Server或Domain Server必须存储与该用户关联的计算机ID。

跟踪计算机ID的最可靠方法是存储 [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) 数据库中的方法。 收到新请求后，使用将请求中的计算机ID与已知的计算机ID进行比较 [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) 执行ID比较以确定ID是否代表同一计算机。 仅当机器ID数量较少时，这种比较才具有实用性。 例如，如果用户在其域中允许使用五台计算机，则您可以在数据库中搜索与用户用户名关联的计算机ID，并获取一小部分数据以进行比较。

对于允许匿名访问的部署，这种比较并不实际。 在这个案例中， [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) 可以使用。 但是，如果用户从Flash和Adobe AIR®运行时访问内容，则此ID不能相同。

>[!NOTE]
>
>如果用户重新格式化硬盘，则ID将无法存留。