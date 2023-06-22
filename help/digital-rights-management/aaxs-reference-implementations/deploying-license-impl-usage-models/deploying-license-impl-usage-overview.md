---
title: 实施使用模型概述
description: 实施使用模型概述
copied-description: true
exl-id: 48e7db54-484f-4c46-9a4e-a51bae7c84b4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# 实施使用模型概述 {#implementing-the-usage-models-overview}

参考实施包括业务逻辑，用于演示如何为打包的内容启用以下四种不同的使用模型：

* 下载到拥有(DTO)
* 租赁/视频点播(VOD)
* 订阅（方便食用）
* 广告融资

要启用使用模型演示，请指定自定义属性 `RI_UsageModelDemo=true` 在打包时。 如果使用Media Packager命令行工具打包内容，请指定：

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>如果您未在打包时激活可选演示模式，则许可证服务器将使用在打包时指定的策略来颁发许可证。 如果指定了多个策略，则许可证服务器将使用第一个有效策略。

在演示中，服务器上的业务逻辑控制生成的许可证的实际属性。 在打包时，内容中必须只包含最少的策略信息。 具体来说，策略只需要指示是否需要进行身份验证才能访问内容。 要启用所有四种使用模型，请包括一个允许匿名访问的策略（对于广告赞助模型）和一个要求用户名/密码身份验证的策略（对于其他3种使用模型）。 当请求许可证时，客户端应用程序可以基于策略中的认证信息确定是否提示用户进行认证。

为了控制使用模型，在该使用模型下向特定用户颁发许可证，可以将条目添加到参考实现数据库中。 此 `Customer` 表包含用于验证用户的用户名和口令。 它还指示用户是否有订阅。 拥有订阅的用户将获得以下项下的许可证： *订阅* 使用模式。 要授予用户访问 *下载到所有者* 或 *点播视频* 使用模型时，可以将条目添加到 `CustomerAuthorization` 表，指定允许用户访问的每个内容块和使用模型。 请参阅 [!DNL PopulateSampleDB.sql] 脚本，以了解有关填充每个表的详细信息。

当用户请求许可证时，参考实施服务器会检查客户端发送的元数据，以确定内容是否使用 `RI_UsageModelDemo` 属性。 如果存在，则使用以下业务规则：

* 如果其中一个策略需要身份验证：

   * 如果请求包含有效的身份验证令牌，请在Customer数据库表中查找用户。 如果找到用户：

      * 如果 `Customer.IsSubscriber` 属性为 `true`，为生成许可证 *订阅* 使用模型并将其发送给用户。

      * 在中查找记录 `CustomerAuthorization` 此用户ID和内容ID的数据库表。 如果找到记录：

         * 如果 `CustomerAuthorization.UsageType` 是 `DTO`，为生成许可证 *下载到所有者* 使用模型并将其发送给用户。

         * 如果 `CustomerAuthorization.UsageType` 是 `VOD`，为生成许可证 *视频点播* 使用模型并将其发送给用户。
   * 如果任何策略都不允许匿名访问：

      * 如果请求中没有有效的身份验证令牌，则返回“需要身份验证”错误。
      * 否则，返回“未授权”错误。


* 如果其中一个策略允许匿名访问，请为广告资助的使用模型生成许可证，并将其发送给用户。

在参考实施服务器可以颁发使用模式演示的许可证之前，需要配置服务器以指定如何为四种使用模式中的每种模式生成许可证。 这是通过为每个使用模型指定策略来完成的。 参考实施包括四个示例策略( [!DNL dto-policy.pol]， [!DNL vod-policy.pol]， [!DNL sub-policy.pol]， [!DNL ad-policy.pol])，或者您可以替换自己的策略。 In [!DNL flashaccess-refimpl.properties]，设置以下属性以指定用于每个使用模式的策略，并将策略文件放置在 `config.resourcesDirectory` 属性：

```
# Policy file name for Download To Own usage  
RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol  
# Policy file name for Rental usage  
RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol  
# Policy file name for Subscription usage  
RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol  
# Policy file name for Ad Supported (free) usage  
RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
```
