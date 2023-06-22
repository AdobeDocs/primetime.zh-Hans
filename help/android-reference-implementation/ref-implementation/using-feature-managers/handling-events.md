---
description: 如果应用程序需要处理从功能管理器调度的事件，则需要在PlayerFragment.java文件中注册管理器。
title: 处理事件
exl-id: 4c9a76bb-071e-4408-819c-a7611fe615cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
