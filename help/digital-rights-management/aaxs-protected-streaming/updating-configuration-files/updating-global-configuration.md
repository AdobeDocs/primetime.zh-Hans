---
title: 更新全局配置文件
description: 更新全局配置文件
copied-description: true
exl-id: 6544d8ae-6d23-498e-92c5-bad6bfcc10ef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# 更新全局配置文件{#updating-the-global-configuration-file}

中的HSM密码 [!DNL flashaccess-global.xml] 可以随时修改，所做的更改将在下次服务器重新加载配置文件时生效。 但是，不会重新加载对“Logging”和“Caching”元素的更改；对这些元素中的任何更改都需要重新启动服务器。
