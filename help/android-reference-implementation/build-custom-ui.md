---
description: 您可以轻松构建基于参考实现框架的自定义用户界面。
title: 构建自定义用户界面
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# 构建自定义用户界面{#build-a-custom-user-interface}

您可以基于参考实现框架构建自定义用户界面。

以下功能的UI组件已集成：

* 可点击广告
* 广告叠加
* 延迟绑定音频
* 隐藏式字幕
* 上述所有组件的监听器

1. 编辑[!DNL PlayerFragment.java]文件以初始化要在播放器中使用的UI组件。

1. 编辑[!DNL res/player/player_fragment.xml]文件以自定义用户界面。
1. 构建项目。

>[!NOTE]
>
>要对搜索栏进行UI更改，可以编辑MarkableSeekBar类。 [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html)类处理滑块、滑块的拇指、标记保持器、提示标记、缓冲区范围和搜索范围背景。