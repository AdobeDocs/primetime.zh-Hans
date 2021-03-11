---
title: 通过HTTPS安全广告加载
description: 通过HTTPS安全广告加载
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# 通过HTTPS{#secure-ad-loading-over-https}安全广告加载

Adobe Primetime提供了通过HTTPS请求对Primetime广告服务器和CRS相关调用的首次调用的选项。

默认情况下不启用该功能。 使用以下工具启用安全广告加载。

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

