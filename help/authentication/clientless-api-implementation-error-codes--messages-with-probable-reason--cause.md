---
title: 无客户端API实施 — 错误代码/具有可能原因/原因的消息
description: 无客户端API实施 — 错误代码/具有可能原因/原因的消息
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# 无客户端API实施 — 错误代码/具有可能原因/原因的消息 {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>


## 错误：未授权

### 原因：

1. POST中缺少授权标头
1. 授权标头问题 — 检查请求时间是否以毫秒为单位。

## 错误：验证期间的SC 400

### 原因：

1. 服务器未找到为特定请求者和环境创建的注册代码。
1. 您可能会遇到跨域脚本问题
1. 应将正确的欺骗添加到/etc/hosts文件

## 错误：400个错误请求

### 原因：

1. POST/GET的URL格式错误
1. SAMLAssertionParserException — 加密的SAML断言在Adobe的末尾无法解密

## 错误：403禁止访问

### 原因：

1. 请求过多 — API管理的一项功能，可阻止DoS攻击。
2. 如果使用预先环境，则添加欺骗，否则，请确保从/etc/hosts文件中删除了欺骗

## 错误：无法登录MVPD页面

### 原因：

1. 用户名和密码不匹配 
2. 登录可能已禁用
3. 检查登录是用于生产还是暂存


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->