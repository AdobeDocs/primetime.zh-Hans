---
title: 存储密钥
description: 存储密钥
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 存储密钥{#store-keys}

Adobe建议内容发布者将用于签名和加密的加密私钥存储在安全、防篡改的硬件设备中。 存储在软件中的密钥比存储在硬件中的密钥更容易受损。 例如，如果某个软件密钥泄露，通常会复制包含该密钥的密钥或文件，从而难以检测到泄露。 存储在硬件上的密钥不易受到未检测到的危害。

硬件安全模块(HSM)是存储和保护加密密钥的专用硬件设备。 有关更多信息，请参阅 *存储凭据* 在 *使用Adobe Primetime DRM SDK保护内容*.
