---
description: 如果应用程序需要处理从功能管理器调度的事件，它需要在PlayerFragment.java文件中注册管理器。
seo-description: 如果应用程序需要处理从功能管理器调度的事件，它需要在PlayerFragment.java文件中注册管理器。
seo-title: 处理事件
title: 处理事件
uuid: 13639f02-0dcc-4a0a-8524-515da5478006
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 处理事件 {#handling-events}

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
