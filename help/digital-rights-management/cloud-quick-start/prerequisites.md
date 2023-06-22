---
title: 先决条件
description: 先决条件
copied-description: true
exl-id: 1b66f7fd-ea2f-4217-b327-910e90ab889d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# 先决条件 {#prerequisites}

在打包内容之前，需要Primetime DRM Packager证书。 必须通过Primetime DRM证书注册过程请求该证书。 只需要打包程序证书（无许可证服务器或传输）。 请在证书请求电子邮件中指明该请求是要与DRM服务一起使用的证书。

[证书注册指南](../../digital-rights-management/certificate-enrollment-guide/about-certs.md)

包装证书分为两个级别 — 生产和试用。 使用试用证书打包的内容仅供开发使用，在证书过期后不会播放。 颁发给“试用版”内容的所有许可证的最大硬编码策略到期日期将等于证书到期日期（如果未在DRM策略中设置）。
