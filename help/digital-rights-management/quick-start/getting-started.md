---
seo-title: 入门
title: 入门
uuid: 2002cf94-c8a7-4820-a560-6d9f7f33ee97
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 入门 {#getting-started}

本文档提供了快速设置和部署Adobe Primetime DRM生态系统的步骤，该生态系统使用渐进式下载来分发内容，Primetime DRM服务器用于受保护的流进行许可证分发。 以下指南提供了有关每个步骤的更多详细信息：

* *使用Primetime DRM Server保护内容*
* *使用Primetime DRM Server实现受保护的流*

Primetime DRM Server for Protected Streaming是一款功能最小且不包含源代码的服务器。 有关具有完整Java源的可修改服务器，请参 *阅使用Primetime DRM Reference Implementations指南* 。 如果您设置了参考许可证服务器，它将替换“设置”和“部 *署Primetime DRM服务器以用于受保护的流（许可证服务器）”步骤* 。

## 先决条件 {#prerequisites}

在开始之前，请完成以下任务：

* 获取两台Windows或Linux计算机：

   * 一台计算机将是许可证服务器。
   * 一台计算机将是Content Server。

* 在两台计算机上安装以下应用程序：

   * Tomcat 6.0.18
   * Java 1.6

## 获取证书 {#obtain-certificates}

在交付SDK软件后，指定的公司证书管理员将收到完成Adobe Primetime DRM证书注册过程的邀请。 有关详细信息，请参 *阅Primetime DRM证书登记指南*。

1. 管理员至少指派一名个人担任证书请求者。
1. 证书请求者生成私钥和CSR。
1. 请求者提交证书请求。
1. 公司管理员批准此请求。
1. Adobe证书管理员将确认提交。
1. 请求者接收证书，将证书与私钥绑定，并部署证书。 如中所述。

   有关部署证书的详细信息，请参 *阅部署Adobe Primetime DRM Server for Protected Streaming* 指南。
1. 必须针对每个证书类型完成步骤3到6。

   对于Primetime DRM制作版本，请求人必须对有效期为两年的许可证服务器、包装和传输证书单独提出请求。

   使用Primetime DRM评估版或试用版的客户只需要一个证书，有效期分别为1年/90天。