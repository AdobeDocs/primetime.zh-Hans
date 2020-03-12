---
description: 您可以轻松构建基于参考实现框架的自定义用户界面。
seo-description: 您可以轻松构建基于参考实现框架的自定义用户界面。
seo-title: 构建自定义用户界面
title: 构建自定义用户界面
uuid: b785f6a4-3ef8-4f7a-a087-0d6551da9750
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 构建自定义用户界面 {#build-a-custom-user-interface}

您可以基于参考实现框架构建自定义用户界面。

以下功能的UI组件已集成：

* 可点击广告
* 广告叠加
* 后期绑定音频
* 隐藏式字幕
* 上述所有组件的监听器

1. 编辑 [!DNL PlayerFragment.java] 文件以初始化要在播放器中使用的UI组件。

1. 编辑文 [!DNL res/player/player_fragment.xml] 件以自定义用户界面。
1. 构建项目。

>[!NOTE]
>
>要对搜索栏进行UI更改，可编辑MarkableSeekBar类。 MarkableSeekBar [](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) 类处理滑块、滑块的缩略图、广告标记保持器、提示标记、缓冲区范围和搜索范围背景。