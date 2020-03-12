---
description: 创建视频分析管理器
seo-description: 创建视频分析管理器
seo-title: 创建视频分析管理器
title: 创建视频分析管理器
uuid: d72e1dfe-df70-47cc-9e00-bd09017d6127
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 创建视频分析管理器 {#create-the-video-analytics-manager}

新的管理器类( `VAManager`)已添加到Android参考实现。 `VAManager` 只需创建并销毁类的实 `VideoHeartbeat` 例。 在创建新实例时， `VAManager` 引用实现会创建一 `MediaPlayer` 个实例，并在破坏实例时 `MediaPlayer` 销毁该实例。 这在中实现 `PlayerFragment.java`。

## 创建新的视频分析管理器

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

config变量是的一个具体实现， `IVAConfig` 包含运行时配 `VideoHeartbeat` 置。

>[!NOTE]
>
>如果Android应用程序未配置Adobe Analytics帐户，则即使创建并启用了某个实例，也不会生成视 `VAManager` 频跟踪数据。

