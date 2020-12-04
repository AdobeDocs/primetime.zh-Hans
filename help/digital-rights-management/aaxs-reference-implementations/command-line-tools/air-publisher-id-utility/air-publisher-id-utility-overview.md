---
seo-title: AIR Publisher ID实用程序概述
title: AIR Publisher ID实用程序概述
uuid: 31aecc0e-ad9b-43ad-ba58-77d2c999f4a4
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# AIR Publisher ID实用程序概述{#air-publisher-id-utility-overview}

作为构建AIR文件过程的一部分，AIR开发人员工具(ADT)生成一个发布者ID。 这是用于构建AIR文件的证书的唯一标识符。 如果对多个AIR应用程序重用同一证书，它们将具有相同的发布者ID。AIR发布者ID实用程序用于计算AIR应用程序的发布者ID。 1.5.2之后的AIR版本不会将生成的发布者ID写入文件，因此，如果您使用的是AIR应用程序允许列表，则必须使用此工具确定发布者ID。

>[!NOTE]
>
>用于AIR允许列表实施的发布者ID与应用程序[!DNL application.xml]文件中应用程序发布者指定的发布者ID不同。
