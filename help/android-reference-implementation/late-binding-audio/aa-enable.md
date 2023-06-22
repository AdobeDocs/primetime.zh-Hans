---
description: 您可以通过创建备用音频功能管理器，将后期绑定或备用音频流集成到播放器中。
title: 集成后期捆绑音频
exl-id: 43be9042-d547-4646-a920-cdd2a5dbb1fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# 集成后期捆绑音频 {#integrate-late-binding-audio}

您可以通过创建备用音频功能管理器，将后期绑定或备用音频流集成到播放器中。

* 要创建备用音频管理器，请执行以下操作：

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* 要使用ManagerFactory启用备用音频，请确保以下代码行位于 `PlayerFragment.java` 文件：

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   禁用备用音频：

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```
