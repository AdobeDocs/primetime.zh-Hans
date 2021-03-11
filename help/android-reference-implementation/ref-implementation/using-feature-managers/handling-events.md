---
description: 如果应用程序需要处理从功能管理器调度的事件，它需要在PlayerFragment.java文件中注册管理器。
title: 处理事件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 4%

---


# 处理事件{#handling-events}

如果应用程序需要处理从功能管理器调度的事件，它需要在PlayerFragment.java文件中注册管理器。

例如：

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```
