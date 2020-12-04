---
description: 'null'
seo-description: 'null'
seo-title: 通过HTTPS安全加载广告
title: 通过HTTPS安全加载广告
uuid: 10657f59-cfbf-4c75-9249-fc154952bc51
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 0%

---


# 通过HTTPS安全加载广告{#secure-ad-loading-over-https}

Adobe Primetime可以通过https请求第三方广告服务器，即使播放器托管在http上也是如此。 只有那些ad-server调用将升级为客户端在Auditude Ad解析程序阶段搜索的https。

>[!NOTE]
>
>此功能不支持Flash。

使用以下工具启用安全广告加载。 默认情况下不启用它。

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
