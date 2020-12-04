---
seo-title: 安全地存储策略
title: 安全地存储策略
uuid: b1ac236f-6637-46d4-8405-a819d6093314
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# 安全地存储策略{#securely-storing-policies}

Adobe访问SDK在开发用于内容打包和策略创建的应用程序方面提供了极大的灵活性。 在创建此类应用程序时，您可能希望允许一些用户创建和修改策略，并限制其他用户，使他们只能将现有策略应用于内容。 如果出现这种情况，您必须实施必要的访问控制，以创建具有不同权限的用户帐户，以便创建策略以及将策略应用到内容。

在打包中使用策略之前，不会对其进行签名或以其他方式保护其不进行修改。 如果您担心打包工具的用户修改策略，应考虑签署策略以确保不能修改它们。

有关使用SDK创建应用程序的详细信息，请参阅&#x200B;*Adobe访问API参考*。
