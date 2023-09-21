---
description: 创建视频分析管理器
title: 创建视频分析管理器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 创建视频分析管理器 {#create-the-video-analytics-manager}

新的经理类( `VAManager`)已添加到Android参考实施。 `VAManager` 只会创建和销毁 `VideoHeartbeat` 类。 引用实施会创建 `VAManager` 新实例时 `MediaPlayer` 创建，并在以下情况下销毁该实例 `MediaPlayer` 已被销毁。 此功能的实现位置 `PlayerFragment.java`.

## 创建新的视频分析管理器

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

配置变量是的具体实施 `IVAConfig` 并包含运行时 `VideoHeartbeat` 配置。

>[!NOTE]
>
>如果Android应用程序未配置Adobe Analytics帐户，那么即使使用的实例，也不会生成视频跟踪数据 `VAManager` 创建并启用。
