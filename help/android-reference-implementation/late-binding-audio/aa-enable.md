---
description: 您可以通过创建替代音频功能管理器将延迟绑定或替代音频流集成到播放器中。
title: 集成后期绑定音频
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# 集成后期绑定音频{#integrate-late-binding-audio}

您可以通过创建替代音频功能管理器将延迟绑定或替代音频流集成到播放器中。

* 要创建替代音频管理器，请执行以下操作：

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* 要使用ManagerFactory启用替代音频，请确保在`PlayerFragment.java`文件中包含以下代码行：

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   要禁用替代音频，请执行以下操作：

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```

