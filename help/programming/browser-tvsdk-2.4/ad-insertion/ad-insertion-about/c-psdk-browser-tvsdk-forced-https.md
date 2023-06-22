---
title: 通过HTTPS的安全广告加载
description: 通过HTTPS的安全广告加载
copied-description: true
exl-id: d43418e9-631b-4344-a5b3-0a6154a325d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# 通过HTTPS的安全广告加载{#secure-ad-loading-over-https}

即使播放器托管在http上，Adobe Primetime也可以通过https请求第三方广告服务器。 在审核广告解析程序阶段，只有这些广告服务器调用会升级到客户端查找的https。

>[!NOTE]
>
>Flash不支持此功能。

使用以下内容启用安全广告加载。 默认情况下不启用该功能。

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
