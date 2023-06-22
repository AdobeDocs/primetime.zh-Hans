---
title: 关于证书
description: 关于证书
copied-description: true
exl-id: 24ca19bb-a71e-461a-9c3c-558d650e2d99
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 关于证书 {#about-certificates}

Adobe Primetime DRM SDK提供以下配置：

* Primetime DRM生产SDK
* Primetime DRM评估SDK
* Primetime DRM试用版SDK

要使用Primetime DRM SDK创建授权服务器，您必须从Adobe获取数字证书。 数字证书（也简称为证书）将实体（例如个人、组织或系统）绑定到特定的公钥和私钥对。 数字证书可以被视为验证个人、系统或组织身份的电子证书。

为了在部署选项中实现最大的灵活性和增强的安全性，Primetime DRM SDK需要四个证书：

* 许可证服务器证书

   SDK使用此证书来签署颁发给客户端的内容许可证。
* Packager证书

   打包（加密）内容时，SDK使用此证书来生成DRM元数据。
* 传输证书

   SDK使用此证书来保护客户端与许可证服务器之间的通信。
* 域CA证书

   想要实施域服务器的客户需要域CA证书。 与其他证书不同，域CA证书不是由Adobe颁发的。

>[!NOTE]
>
>对于Evaluation SDK和Trial SDK，许可证服务器、Packager和传输证书将合并为单个证书。
