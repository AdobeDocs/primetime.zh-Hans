---
title: 通过HTTPS安全广告加载
description: 通过HTTPS安全广告加载
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# 通过HTTPS{#secure-ad-loading-over-https}安全广告加载

Adobe Primetime可以通过https请求第三方广告服务器，即使播放器是在http上托管的。 只有那些ad-server调用将升级到客户端在Auditude Ad解析程序阶段搜索的https。

>[!NOTE]
>
>此功能不支持Flash。

使用以下工具启用安全广告加载。 默认情况下不启用。

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
