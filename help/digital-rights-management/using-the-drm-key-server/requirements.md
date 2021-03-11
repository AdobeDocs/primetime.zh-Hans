---
title: 使用Primetime DRM Key Server的要求
description: 使用Primetime DRM Key Server的要求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# 简介{#introduction}

Primetime DRM密钥服务器是用于远程iOS和/或Xbox 360密钥投放的多租户密钥服务器。 如果在iOS策略中启用了“远程密钥投放”，则必须部署Primetime DRM密钥服务器才能在iOS客户端上启用内容回放。 Xbox 360始终需要Primetime DRM密钥服务器。

## 使用Primetime DRM密钥服务器{#requirements-for-using-primetime-drm-key-server}的要求

使用Primetime DRM Key Server的最低要求是：

* [Java JRE 1.6或更](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 高版本。（要在Windows 64位上使用HSM，需要JRE 8）

   >[!NOTE]
   >
   >64位PKCS11现在在OpenJDK 8中受支持：[https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131)和Oracle JDK:[https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559)。

* [Apache Tomcat 7](https://tomcat.apache.org)
* 由Adobe发出的凭据
* 由Microsoft颁发的凭据（针对Xbox 360客户端）