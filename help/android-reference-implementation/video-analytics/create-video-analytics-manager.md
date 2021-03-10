---
description: 创建视频分析管理器
title: 创建视频分析管理器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# 创建Video Analytics Manager {#create-the-video-analytics-manager}

新的管理器类(`VAManager`)已添加到Android Reference Implementation。 `VAManager` 简单地创建和销毁类的实 `VideoHeartbeat` 例。引用实现在创建新`MediaPlayer`时创建`VAManager`实例，并在`MediaPlayer`被破坏时销毁该实例。 这在`PlayerFragment.java`中实现。

## 要创建新的Video Analytics Manager

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

config变量是`IVAConfig`的具体实现，包含运行时`VideoHeartbeat`配置。

>[!NOTE]
>
>如果Android应用程序未配置Adobe Analytics帐户，则不会生成视频跟踪数据，即使已创建并启用`VAManager`实例也是如此。

