---
title: 快速入门
description: 快速入门
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# 快速入门 {#getting-started}

本文档提供了快速设置和部署Adobe Primetime DRM生态系统的步骤，该生态系统使用渐进式下载来分发内容，并使用Primetime DRM Server for Protected Streaming来分发许可证。 以下指南中提供了有关每个步骤的其他详细信息：

* *使用Primetime DRM服务器保护内容*
* *使用用于受保护流的Primetime DRM服务器*

Primetime DRM Server for Protected Streaming是功能最少的服务器，不包含源代码。 对于具有完整Java源的可修改服务器，请参见 *使用Primetime DRM参考实施* 指南。 如果设置了“参照许可证”服务器，它将替换 *设置和部署Primetime DRM Server for Protected Streaming（许可证服务器）* 步骤。

## 先决条件 {#prerequisites}

在开始之前，请完成以下任务：

* 获取两台Windows或Linux计算机：

   * 一台计算机将成为许可证服务器。
   * 一台计算机将成为Content Server。

* 在两个计算机上安装以下应用程序：

   * Tomcat 6.0.18
   * Java 1.6

## 获取证书 {#obtain-certificates}

交付SDK软件后，指定的公司证书管理员将收到一封邀请函，邀请其完成Adobe Primetime DRM证书注册流程。 欲了解更多信息，请参见 *Primetime DRM证书注册指南*.

1. 管理员至少指派一名个人担任证书请求者。
1. 证书请求者生成私钥和CSR。
1. 请求者提交证书请求。
1. 公司管理员批准该请求。
1. Adobe证书管理员将确认提交。
1. 请求者接收证书、将证书与私钥绑定并部署证书。 如中所述。

   有关部署证书的详细信息，请参阅 *为受保护的流部署Adobe Primetime DRM Server* 指南。
1. 每种证书类型都必须完成步骤3至6。

   对于Primetime DRM Production版本，请求者必须单独请求有效期为两年的许可证服务器、包装和传输证书。

   使用Primetime DRM评估版或试用版的客户只需要一个证书，其有效期分别为1年/90天。
