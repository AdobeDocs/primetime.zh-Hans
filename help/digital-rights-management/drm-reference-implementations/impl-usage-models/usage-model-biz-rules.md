---
title: 使用模型演示业务规则
description: 使用模型演示业务规则
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# 使用模型演示业务规则{#usage-model-demo-business-rules}

当用户请求许可证时，Reference Implementation服务器将检查客户端发送的元数据，以确定内容是否使用`RI_UsageModelDemo`属性打包。 如果是，则服务器应用以下业务规则。

* 如果DRM策略之一需要身份验证：

   * 如果请求包含有效的身份验证令牌，请在Customer数据库表中搜索用户的名称。

      如果找不到用户的名称，请完成以下任务:

      * 如果`Customer.IsSubscriber`属性设置为`true`，则需要为&#x200B;*`Subscription`*&#x200B;使用模型生成许可证并将其发送给用户。

      * 在`CustomerAuthorization`数据库表中搜索记录，以查找用户名和内容ID。

      如果可以找到用户记录，请完成以下任务:

      * 如果`CustomerAuthorization.UsageType`属性设置为`DTO`，则为DTO使用模型生成许可证并将其发送给用户。

      * 如果将`CustomerAuthorization.UsageType`属性设置为`VOD`，则为VOD使用模型生成许可证并将其发送给用户。

      如果所有DRM策略都不允许匿名访问，请完成以下任务:

      * 如果请求中没有有效的身份验证令牌，您需要返回“需要身份验证”错误。
      * 否则，返回“未授权”错误。



* 如果DRM策略之一允许匿名访问，请为广告资助的使用模式生成许可证并发送给用户。

