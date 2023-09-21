---
title: 通过HTTPS安全加载广告
description: 通过HTTPS安全加载广告
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# 通过HTTPS安全加载广告{#secure-ad-loading-over-https}

即使播放器托管在http上，Adobe Primetime也可以通过https请求第三方广告服务器。 只有这些ad-server调用才会升级到Auditude广告解析程序阶段客户端查找的https。

>[!NOTE]
>
>Flash不支持此功能。

使用以下内容启用安全广告加载。 默认情况下不启用此功能。

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
