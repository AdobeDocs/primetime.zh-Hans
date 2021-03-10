---
description: 如果业务规则要求跟踪用户的计算机数，则许可证服务器或域服务器必须存储与用户关联的计算机ID。
title: 颁发许可证时的计算机计数
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# 颁发许可证{#machine-count-when-issuing-licenses}时的计算机计数

如果业务规则要求跟踪用户的计算机数，则许可证服务器或域服务器必须存储与用户关联的计算机ID。

跟踪机器ID的最可靠方法是将[MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes())方法返回的值存储在数据库中。 收到新请求后，请使用[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId))将请求中的计算机ID与已知的计算机ID进行比较。

[MachineId.matches()执](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) 行ID比较以确定ID是否表示同一计算机。此比较仅在机器ID数较少时才可用。 例如，如果允许用户在其域中使用五台计算机，则可以在数据库中搜索与用户用户名关联的计算机ID，并获取一小组数据进行比较。

此比较对于允许匿名访问的部署而言不实用。 在这种情况下，可以使用[MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())。 但是，如果用户从Flash和Adobe AIR®运行时访问内容，则此ID不能相同。

>[!NOTE]
>
>如果用户重新格式化硬盘，该ID将不会存在。