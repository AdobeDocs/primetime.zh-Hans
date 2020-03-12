---
seo-title: 使用Primetime DRM Key Server的要求
title: 使用Primetime DRM Key Server的要求
uuid: 769f9e10-7a3e-4a38-b30d-18181b666bb4
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# 简介 {#introduction}

Primetime DRM Key Server是用于远程iOS和／或Xbox 360密钥交付的多租户密钥服务器。 如果在iOS策略中启用了“远程密钥交付”，则必须部署Primetime DRM密钥服务器才能在iOS客户端上启用内容回放。 Primetime DRM Key Server始终是Xbox 360的必需工具。

## 使用Primetime DRM Key Server的要求 {#requirements-for-using-primetime-drm-key-server}

使用Primetime DRM Key Server的最低要求是：

* [Java JRE 1.6或更高版本](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 。 （要在Windows 64位上使用HSM，需要JRE 8）

   >[!NOTE]
   >
   >64位PKCS11现在在OpenJDK 8中受支持： [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131)，和Oracle JDK: [https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559)。

* [Apache Tomcat 7](https://tomcat.apache.org)
* Adobe颁发的凭据
* 由Microsoft颁发的凭据（针对Xbox 360客户端）