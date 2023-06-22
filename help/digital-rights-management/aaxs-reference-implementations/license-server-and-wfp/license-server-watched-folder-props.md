---
title: 观察文件夹属性
description: 观察文件夹属性
copied-description: true
exl-id: e86518d4-2a16-45c7-aa96-189f677c3ee6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 观察文件夹属性 {#watched-folder-properties}

每个观察文件夹都包含一个名为的文件 [!DNL properties/watchfolder.properties]. 此文件包含放置在此文件夹中的内容的打包选项，包括要加密的内容以及要应用的策略。 对属性文件中的值所做的任何更改都将在下次运行watched文件夹打包程序时生效（无需重新启动服务器）。

如果打包程序属性文件中存在配置错误，则打包程序线程将停止。 要继续观察文件夹打包程序，请重新启动服务器。 如果watched文件夹属性文件中存在配置错误，则会从打包程序处理的文件夹列表中临时删除watched文件夹。 要将watched文件夹添加回列表，请重新启动服务器或修改打包程序属性文件。 如果在打包特定文件时发生错误（例如，由于文件损坏），将跳过该文件并处理文件夹中的其余文件。
