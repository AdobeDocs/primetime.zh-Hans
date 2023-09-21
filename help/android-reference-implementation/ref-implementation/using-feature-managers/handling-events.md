---
description: 如果应用程序需要处理从功能管理器调度的事件，则需要在PlayerFragment.java文件中注册管理器。
title: 处理事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# 处理事件 {#handling-events}

如果应用程序需要处理从功能管理器调度的事件，则需要在PlayerFragment.java文件中注册管理器。

例如：

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```
