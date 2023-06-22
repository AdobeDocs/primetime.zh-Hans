---
description: 您可以基于参考实施框架轻松构建自定义用户界面。
title: 构建自定义用户界面
exl-id: 96008010-cd63-4fb1-a3fc-2fc94b624413
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 构建自定义用户界面 {#build-a-custom-user-interface}

您可以基于参考实施框架构建自定义用户界面。

已集成以下功能的UI组件：

* 可点击广告
* 广告叠加图
* 后期绑定音频
* 隐藏字幕
* 以上所有组件的监听器

1. 编辑 [!DNL PlayerFragment.java] 文件，用于初始化要在播放器中使用的UI组件。

1. 编辑 [!DNL res/player/player_fragment.xml] 文件，以自定义用户界面。
1. 生成项目。

>[!NOTE]
>
>要对搜寻栏进行UI更改，可以编辑MarkableSeekBar类。 此 [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) 类处理滑块、滑块缩略图、广告标记载体、提示标记、缓冲范围和搜寻范围背景。
