---
description: 您可以通过创建替代音频功能管理器将后期绑定或替代音频流集成到播放器中。
seo-description: 您可以通过创建替代音频功能管理器将后期绑定或替代音频流集成到播放器中。
seo-title: 集成后期绑定音频
title: 集成后期绑定音频
uuid: cd2e259a-2af4-4d7b-a856-79bd087e8ca6
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 集成后期绑定音频 {#integrate-late-binding-audio}

您可以通过创建替代音频功能管理器将后期绑定或替代音频流集成到播放器中。

* 要创建替代音频管理器，请执行以下操作：

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* 要使用ManagerFactory启用替代音频，请确保文件中包含以下代 `PlayerFragment.java` 码行：

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   要禁用替代音频，请执行以下操作：

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```

