---
description: 'null'
seo-description: 'null'
seo-title: 通过HTTPS安全加载广告
title: 通过HTTPS安全加载广告
uuid: 72ab94d3-ee0c-4f02-adf2-c186ae6aec26
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 通过HTTPS安全加载广告 {#secure-ad-loading-over-https}

Adobe Primetime提供了通过HTTPS请求对Primetime广告服务器和CRS相关调用的首次调用的选项。

默认情况下，该功能未启用。 使用以下内容启用安全广告加载。

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

