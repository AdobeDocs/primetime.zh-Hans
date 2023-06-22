---
title: 通过HTTPS的安全广告加载
description: 通过HTTPS的安全广告加载
copied-description: true
exl-id: e12cb9d4-05d4-485e-b629-1af680b83e04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# 通过HTTPS的安全广告加载{#secure-ad-loading-over-https}

Adobe Primetime提供了一个选项，用于通过HTTPS请求首次调用Primetime广告服务器和CRS相关调用。

默认情况下不启用该功能。 使用以下内容启用安全广告加载。

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
