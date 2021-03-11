---
title: 监视文件夹属性
description: 监视文件夹属性
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# 监视文件夹属性{#watched-folder-properties}

每个监视文件夹都包含一个名为[!DNL properties/watchfolder.properties]的文件。 此文件包含放置在此文件夹中的内容的打包选项，包括要加密的内容以及要应用的策略。 对属性文件中的值所做的任何更改将在下次运行监视的文件夹打包程序时生效（无需重新启动服务器）。

如果打包程序属性文件中存在配置错误，打包程序线程将停止。 要恢复监视的文件夹打包程序，请重新启动服务器。 如果监视文件夹属性文件中存在配置错误，则从打包程序进程的文件夹列表中临时删除监视文件夹。 要将监视的文件夹添加回列表，请重新启动服务器或修改打包程序属性文件。 如果在打包特定文件时出错（例如，由于文件已损坏），将跳过该文件，并处理该文件夹中的其余文件。
