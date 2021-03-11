---
title: 关于证书
description: 关于证书
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# 关于证书{#about-certificates}

Adobe Primetime DRM SDK有以下配置：

* Primetime DRM制作SDK
* Primetime DRM评估SDK
* Primetime DRM试用版SDK

要使用Primetime DRM SDK创建许可服务器，您必须从Adobe获得数字证书。 数字证书（也称为证书）将实体（如个人、组织或系统）绑定到特定的公共和私钥对。 数字证书可以视为验证个人、系统或组织身份的电子凭据。

为了在您的部署选项中实现最大的灵活性和增强的安全性，Primetime DRM SDK需要四个证书：

* 许可证服务器证书

   SDK使用此证书签署颁发给客户的内容许可。
* 包装程序证书

   SDK在打包（加密）内容时使用此证书生成DRM元数据。
* 传输证书

   SDK使用此证书保护客户端与许可证服务器之间的通信。
* 域CA证书

   要实施域服务器的客户需要域CA证书。 与其他证书不同，域CA证书不是由Adobe颁发的。

>[!NOTE]
>
>对于评估版SDK和试用版SDK，许可证服务器、包装程序和传输证书将合并到单个证书中。

