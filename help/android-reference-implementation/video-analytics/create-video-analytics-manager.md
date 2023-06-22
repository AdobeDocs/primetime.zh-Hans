---
description: 创建视频分析管理器
title: 创建视频分析管理器
exl-id: 8d2bbb39-10e2-43e8-8ed3-bc376b3f3cc8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 创建视频分析管理器 {#create-the-video-analytics-manager}

新的经理类( `VAManager`)已添加到Android参考实施。 `VAManager` 只是创建和销毁 `VideoHeartbeat` 类。 引用实施会创建 `VAManager` 新实例时 `MediaPlayer` 创建，并在以下情况下销毁该实例： `MediaPlayer` 已被销毁。 此功能的实现位置 `PlayerFragment.java`.

## 创建新的视频分析管理器

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

config变量是的具体实现 `IVAConfig` 并包含运行时 `VideoHeartbeat` 配置。

>[!NOTE]
>
>如果Android应用程序未使用Adobe Analytics帐户配置，则不会生成视频跟踪数据，即使是 `VAManager` 创建并启用。
