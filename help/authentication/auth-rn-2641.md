---
title: Adobe Primetime authentication 2.64.1发行说明
description: Adobe Primetime authentication 2.64.1发行说明
exl-id: b0edbd90-ebb5-40a7-9034-1699dccfadb5
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Adobe Primetime authentication 2.64.1发行说明 {#authn-264-rn}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

本页介绍了此版本的新增功能、更改和已知问题：

## 服务器端和Web客户端 {#server-side-web-clients-2641}

* [内部版本号](#build-number-2641)
* [发行版概述](#release-overview-2641)

### 内部版本号 {#build-number-2641}

Adobe Primetime身份验证： adobe-pass-**2.64.1**
发行日期： **01/31/2023 - 02/02/2023**

### 发行版概述 {#release-overview-2641}

此版本添加了以下内容：

* 能够阻止来自MVPD的未经请求的身份验证响应，其中SAML断言中缺少“in_response_to”参数。
* 改进了对redirect_url参数的验证，以符合安全要求。
* 改进了使用从初始设备提供的信息来记录用于第二屏幕认证请求的设备信息。
