---
title: 入门
description: 入门
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# 入门{#getting-started}

本文档提供了快速设置和部署Adobe Primetime DRM生态系统的步骤，该生态系统使用渐进式下载来分发内容，而Primetime DRM服务器用于受保护流以分发许可证。 以下指南提供了有关每个步骤的更多详细信息：

* *使用Primetime DRM Server保护内容*
* *使用Primetime DRM Server实现受保护的流*

Primetime DRM Server for Protected Streaming是一款功能最小、不包含源代码的服务器。 有关具有完整Java源的可修改服务器，请参阅&#x200B;*使用Primetime DRM参考实现*&#x200B;指南。 如果设置参考许可证服务器，则替代了&#x200B;*设置和部署Primetime DRM Server for Protected Streaming(License Server)*&#x200B;步骤。

## 先决条件{#prerequisites}

在开始之前，请完成以下任务:

* 获取两台Windows或Linux计算机：

   * 一台计算机将是许可证服务器。
   * 一台计算机将是Content Server。

* 在两台计算机上安装以下应用程序：

   * Tomcat 6.0.18
   * Java 1.6

## 获取证书{#obtain-certificates}

交付SDK软件后，指定的公司证书管理员将收到完成Adobe Primetime DRM证书注册过程的邀请。 有关详细信息，请参阅&#x200B;*Primetime DRM证书注册指南*。

1. 管理员指定至少一人担任证书请求者。
1. 证书请求者生成私钥和CSR。
1. 请求者提交证书请求。
1. 公司管理员批准该请求。
1. Adobe证书管理员确认提交。
1. 请求者接收证书，将证书与私钥绑定，并部署证书。 如中所述。

   有关部署证书的详细信息，请参阅&#x200B;*部署Adobe Primetime DRM Server for Protected Streaming*&#x200B;指南。
1. 必须针对每个证书类型完成步骤3至6。

   对于Primetime DRM制作版本，申请人必须对有效期为两年的许可证服务器、包装和传输证书单独提出请求。

   使用Primetime DRM评估版或试用版的客户只需要一份证书，有效期分别为1年/90天。