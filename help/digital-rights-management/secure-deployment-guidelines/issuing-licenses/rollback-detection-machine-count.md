---
description: 如果业务规则要求跟踪用户的计算机数，则许可证服务器或域服务器必须存储与用户关联的计算机ID。
seo-description: 如果业务规则要求跟踪用户的计算机数，则许可证服务器或域服务器必须存储与用户关联的计算机ID。
seo-title: 颁发许可证时的计算机计数
title: 颁发许可证时的计算机计数
uuid: 7ba8a8d4-a31f-4f37-82a7-755cfa443544
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 颁发许可证时的计算机计数 {#machine-count-when-issuing-licenses}

如果业务规则要求跟踪用户的计算机数，则许可证服务器或域服务器必须存储与用户关联的计算机ID。

跟踪机器ID的最可靠方法是将 [MachineId.getBytes()方法返回的值存储在数据库中](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) 。 收到新请求后，请使用 [MachineId.matches()将请求中的计算机ID与已知的计算机ID进行比较](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId))。

[MachineId.matches()执行ID比较](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) ，以确定ID是否代表同一台计算机。 此比较仅在机器ID数量较少时才可用。 例如，如果用户在其域中被允许使用五台计算机，则可以在数据库中搜索与用户用户名关联的计算机ID，并获取一小组数据进行比较。

此比较对于允许匿名访问的部署来说不现实。 在这种情况下， [可以使用MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) 。 但是，如果用户从Flash和Adobe AIR®运行时访问内容，则此ID不能相同。

>[!NOTE]
>
>如果用户重新设置硬盘的格式，则ID将不再有效。