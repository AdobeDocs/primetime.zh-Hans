---
title: 安全地存储策略
description: 安全地存储策略
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# 安全地存储策略{#securely-storing-policies}

Adobe Access SDK在开发用于内容打包和策略创建的应用程序方面提供了极大的灵活性。 创建此类应用程序时，您可能希望允许某些用户创建和修改策略，并限制其他用户，以便他们只能将现有策略应用于内容。 如果是这种情况，您必须实施必要的访问控制，以创建具有不同权限的用户帐户，以便创建策略以及将策略应用于内容。

在打包中使用策略之前，不会对其进行签名或以其他方式保护其不进行修改。 如果您担心打包工具的用户修改策略，应考虑对策略进行签名，以确保不能修改这些策略。

有关使用SDK创建应用程序的详细信息，请参阅&#x200B;*Adobe访问API参考*。
