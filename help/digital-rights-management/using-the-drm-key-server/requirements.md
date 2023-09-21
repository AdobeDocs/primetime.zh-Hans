---
title: 使用Primetime DRM Key Server的要求
description: 使用Primetime DRM Key Server的要求
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# 介绍 {#introduction}

Primetime DRM Key Server是用于远程iOS和/或Xbox 360密钥交付的多租户密钥服务器。 如果在iOS的策略中启用了远程密钥交付，则必须部署Primetime DRM密钥服务器，才能在iOS客户端上启用内容播放。 Xbox 360始终需要Primetime DRM密钥服务器。

## 使用Primetime DRM Key Server的要求 {#requirements-for-using-primetime-drm-key-server}

使用Primetime DRM密钥服务器的最低要求如下：

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 或更高版本。 （要在Windows 64位上使用HSM，需要JRE 8）

  >[!NOTE]
  >
  >OpenJDK 8现在支持64位PKCS11： [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131)、和Oracle
* [Apache Tomcat 7](https://tomcat.apache.org)
* 由Adobe颁发的凭据
* Microsoft颁发的凭据（适用于Xbox 360客户端）
