---
description: 'null'
seo-description: 'null'
seo-title: 通过HTTPS安全加载广告
title: 通过HTTPS安全加载广告
uuid: 10657f59-cfbf-4c75-9249-fc154952bc51
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 通过HTTPS安全加载广告{#secure-ad-loading-over-https}

Adobe Primetime可以通过https请求第三方广告服务器，即使播放器是在http上托管的。 只有那些ad-server调用将升级到客户端在Auditude Ad解析程序阶段搜索的https。

>[!NOTE]
>
>Flash不支持此功能。

使用以下内容启用安全广告加载。 默认情况下不启用它。

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
