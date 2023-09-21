---
title: 使用模型演示业务规则
description: 使用模型演示业务规则
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# 使用模型演示业务规则{#usage-model-demo-business-rules}

当用户请求许可证时，参考实现服务器检查客户端已发送的元数据，以确定内容是否通过使用 `RI_UsageModelDemo` 属性。 如果是这种情况，服务器将应用以下业务规则。

* 如果其中一个DRM策略需要身份验证：

   * 如果请求包含有效的身份验证令牌，请在Customer数据库表中搜索用户的名称。

     如果找不到用户的名称，请完成以下任务：

      * 如果 `Customer.IsSubscriber` 属性设置为 `true`，您需要为生成许可证 *`Subscription`* 使用模型并将其发送给用户。

      * 在中搜索记录 `CustomerAuthorization` 用户名称和内容ID的数据库表。

     如果可以找到用户的记录，请完成以下任务：

      * 如果 `CustomerAuthorization.UsageType` 属性设置为 `DTO`，为DTO使用模型生成许可证并将其发送给用户。

      * 如果 `CustomerAuthorization.UsageType` 属性设置为 `VOD`，为VOD使用模型生成许可证并将其发送给用户。

     如果任何DRM策略都不允许匿名访问，请完成以下任务：

      * 如果请求中没有有效的身份验证令牌，则需要返回“需要身份验证”错误。
      * 否则，返回“未授权”错误。

* 如果DRM策略之一允许匿名访问，则为广告资助的使用模型生成许可证并将其发送给用户。
