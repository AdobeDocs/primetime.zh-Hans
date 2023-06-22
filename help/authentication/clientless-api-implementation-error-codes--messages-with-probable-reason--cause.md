---
title: 无客户端API实施 — 错误代码/消息及可能的原因/原因
description: 无客户端API实施 — 错误代码/消息及可能的原因/原因
exl-id: 616e35fc-9b72-422b-9a05-e6248bd52490
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 无客户端API实施 — 错误代码/消息及可能的原因/原因 {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

</br>


## 错误：未授权

### 原因：

1. POST中缺少授权标头
1. 授权标头问题 — 检查请求时间是否以毫秒为单位。

## 错误：SC 400正在进行身份验证

### 原因：

1. 服务器未找到为特定请求者和环境创建的注册码。
1. 您可能会遇到跨域脚本问题
1. 应向/etc/hosts文件中添加适当的欺骗

## 错误： 400错误请求

### 原因：

1. POST/GET的URL格式不正确
1. SAMLAssertionParserException — 加密的SAML断言无法在Adobe末尾解密

## 错误： 403禁止访问

### 原因：

1. 快速请求过多 — API管理的一项功能，用于防御DoS攻击。
2. 如果使用前驱环境，请添加欺骗，否则请确保已从/etc/hosts文件中删除欺骗

## 错误：无法登录到MVPD页

### 原因：

1. 用户名和密码不匹配 
2. 登录可能已被禁用
3. 检查登录是用于生产还是暂存


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->
