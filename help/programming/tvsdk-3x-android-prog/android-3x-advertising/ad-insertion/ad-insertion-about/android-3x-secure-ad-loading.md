---
description: 'null'
seo-description: 'null'
seo-title: 通过HTTPS安全加载广告
title: 通过HTTPS安全加载广告
uuid: 18be77cc-c59b-4982-b8c1-e4451495edd2
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 通过HTTPS安全加载广告 {#secure-ad-loading-over-https}

Adobe Primetime提供了通过HTTPS请求对Primetime广告服务器和CRS相关调用的首次调用的选项。

默认情况下，该功能未启用。 使用以下内容启用安全广告加载。

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
