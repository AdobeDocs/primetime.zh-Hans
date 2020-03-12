---
description: 'null'
seo-description: 'null'
seo-title: 使用模型演示业务规则
title: 使用模型演示业务规则
uuid: c55f85be-5ecb-4a78-b47d-7001ec207d3a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用模型演示业务规则{#usage-model-demo-business-rules}

当用户请求许可证时，参考实施服务器检查客户端发送的元数据，以确定内容是否使用属性进行打 `RI_UsageModelDemo` 包。 如果是，则服务器应用以下业务规则。

* 如果某个DRM策略需要身份验证：

   * 如果请求包含有效的身份验证令牌，请在“客户”数据库表中搜索用户的名称。

      如果找不到用户的名称，请完成以下任务：

      * 如果将 `Customer.IsSubscriber` 该属性设置为 `true`，则需要为使用模型生成许可证， *`Subscription`* 然后将其发送给用户。

      * 在数据库表中搜 `CustomerAuthorization` 索用户名和内容ID的记录。
      如果可以找到用户记录，请完成以下任务：

      * 如果将 `CustomerAuthorization.UsageType` 该属性设置为， `DTO`则为DTO使用模型生成许可证并将其发送给用户。

      * 如果将 `CustomerAuthorization.UsageType` 该属性设置为， `VOD`则为VOD使用模型生成许可证并将其发送给用户。
      如果所有DRM策略都不允许匿名访问，请完成以下任务：

      * 如果请求中没有有效的身份验证令牌，您需要返回“需要身份验证”错误。
      * 否则，返回“未授权”错误。



* 如果某个DRM策略允许匿名访问，请为由广告资助的使用模型生成许可证并将其发送给用户。

