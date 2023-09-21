---
title: AIR Publisher ID实用程序概述
description: AIR Publisher ID实用程序概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# AIR Publisher ID实用程序概述 {#air-publisher-id-utility-overview}

在构建AIR文件的过程中，AIR开发人员工具(ADT)会生成发布者ID。 这是用于构建AIR文件的证书的唯一标识符。 如果您在多个AIR应用程序上重复使用相同的证书，则它们将具有相同的发布者ID。AIR发布者ID实用程序用于计算AIR应用程序的发布者ID。 1.5.2之后的AIR版本不会将生成的发布者ID写入文件，因此如果您使用的是AIR应用程序允许列表，则必须使用此工具来确定发布者ID。

>[!NOTE]
>
>用于实施AIR允许列表的发布者ID与应用程序发布者在应用程序的 [!DNL application.xml] 文件。
