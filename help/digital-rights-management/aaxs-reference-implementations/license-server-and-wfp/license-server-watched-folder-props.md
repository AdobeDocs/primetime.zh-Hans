---
title: 观察文件夹属性
description: 观察文件夹属性
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 观察文件夹属性 {#watched-folder-properties}

每个观察文件夹都包含一个名为 [!DNL properties/watchfolder.properties]. 此文件包含用于打包放置在此文件夹中的内容的选项，包括要加密的内容以及要应用的策略。 对属性文件中的值所做的任何更改将在下次运行观察文件夹打包程序时生效（无需重新启动服务器）。

如果打包程序属性文件中存在配置错误，则打包程序线程将停止。 要继续观察文件夹打包程序，请重新启动服务器。 如果监视文件夹属性文件中存在配置错误，则将从打包程序处理的文件夹列表中临时删除监视文件夹。 要将watched文件夹添加回列表，请重新启动服务器或修改打包程序属性文件。 如果在打包特定文件期间发生错误（例如，由于文件损坏），将跳过该文件并处理文件夹中的其余文件。
