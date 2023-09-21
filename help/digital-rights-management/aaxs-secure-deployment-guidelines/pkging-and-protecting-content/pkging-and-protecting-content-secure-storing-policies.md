---
title: 安全存储策略
description: 安全存储策略
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 安全存储策略{#securely-storing-policies}

Adobe访问SDK在开发用于内容打包和策略创建的应用程序时提供了极大的灵活性。 在创建此类应用程序时，您可能希望允许某些用户创建和修改策略，并限制其他用户以便他们只能将现有策略应用于内容。 如果是这种情况，您必须实施必要的访问控制，以创建具有不同权限的用户帐户，以便创建策略并将策略应用到内容。

在策略用于打包之前，不会对其进行签名或以其他方式保护策略不被修改。 如果您担心打包工具的用户正在修改策略，则应当考虑签署策略以确保无法修改它们。

有关使用SDK创建应用程序的更多信息，请参阅 *Adobe访问API参考*.
