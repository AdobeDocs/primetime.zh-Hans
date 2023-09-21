---
title: 通过HTTPS安全加载广告
description: 通过HTTPS安全加载广告
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# 通过HTTPS安全加载广告 {#secure-ad-loading-over-https}

Adobe Primetime提供了一个选项，用于通过HTTPS请求首次调用Primetime广告服务器以及与CRS相关的调用。

默认情况下，该功能未启用。 使用以下内容启用安全广告加载。

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
