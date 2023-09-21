---
title: Adobe Primetime authentication 2.64发行说明
description: Adobe Primetime authentication 2.64发行说明
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Adobe Primetime authentication 2.64发行说明 {#authn-264-rn}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权使用。

本页介绍了此版本的新增功能、更改和已知问题：

## 服务器端和Web客户端 {#ss-web-clients}

* [内部版本号](#build-no-264)
* [新增功能](#new-featres-264)
* [错误修复](#bug-fixes-264)


### 内部版本号 {#build-no-264}

Adobe Primetime身份验证： adobe-pass-**2.64**

发行日期： **11/08/2022 - 11/10/2022**

### 新增功能 {#new-featres-264}

* 基础架构更新，旨在缩短服务器响应时间，提高系统整体性能。
* 改进了新的平台识别机制。
* 能够阻止来自MVPD的未经请求的身份验证响应，其中SAML断言中缺少“in_response_to”参数。

### 错误修复 {#bug-fixes-264}

* 修复了某些旧版TempPass令牌的格式不正确的问题。
* 解决了第二个屏幕身份验证流程中的轻微问题。
