---
seo-title: 实施使用模型概述
title: 实施使用模型概述
uuid: 1041bb84-9996-4284-b2a0-d6fc6d4b73d9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 实施使用模型概述 {#implementing-the-usage-models-overview}

参考实施包括业务逻辑，用于演示如何为一段打包内容启用以下四种不同的使用模型：

* 下载自带(DTO)
* 租赁／视频点播(VOD)
* 订阅（您可以享用的所有功能）
* 广告资助

要启用使用模型演示，请在打包时指定 `RI_UsageModelDemo=true` 自定义属性。 如果使用Media Packager命令行工具打包内容，请指定：

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>如果您在打包时不激活可选的演示模式，则许可证服务器将使用打包时指定的策略发布许可证。 如果指定了多个策略，则许可证服务器使用第一个有效策略。

在演示中，服务器上的业务逻辑控制生成的许可证的实际属性。 在打包时，内容中只能包含最少的策略信息。 具体而言，策略只需要指示是否需要身份验证才能访问内容。 要启用所有四种使用模式，请包括一项允许匿名访问的策略（针对广告资助的模式）和一项要求用户名／密码身份验证的策略（针对其他3种使用模式）。 当请求许可证时，客户端应用程序可以基于策略中的认证信息确定是否提示用户进行认证。

为了控制将向特定用户颁发许可证的使用模式，可将条目添加到参考实施数据库。 该表 `Customer` 包含用于验证用户的用户名和密码。 它还指示用户是否有订阅。 具有订阅的用户将根据订阅使用模式获 *得许* 可证。 要授予用户在“下载到 *Own* ”或“ *Video on Demand*`CustomerAuthorization` ”使用模型下的访问权限，可向表中添加一个条目，该条目指定允许用户访问的每段内容和使用模型。 有关填充 [!DNL PopulateSampleDB.sql] 每个表的详细信息，请参阅脚本。

当用户请求许可证时，参考实施服务器检查客户端发送的元数据以确定内容是否使用属性进行打 `RI_UsageModelDemo` 包。 如果是，则使用以下业务规则：

* 如果其中一个策略需要身份验证：

   * 如果请求包含有效的身份验证令牌，请在“客户”数据库表中查找用户。 如果找到用户：

      * 如果属 `Customer.IsSubscriber` 性为 `true`Subscription使用模型生成许可证 ** ，然后将其发送给用户。

      * 在数据库表中查找此 `CustomerAuthorization` 用户和内容ID的记录。 如果找到记录：

         * 如果 `CustomerAuthorization.UsageType` 是， `DTO`请为“下载到自己”使 *用模式生成许可证* ，并将其发送给用户。

         * 如果 `CustomerAuthorization.UsageType` 是， `VOD`请为视频点播使用模型生 *成许可证* ，然后将其发送给用户。
   * 如果所有策略都不允许匿名访问：

      * 如果请求中没有有效的身份验证令牌，则返回“需要身份验证”错误。
      * 否则，返回“未授权”错误。


* 如果其中一项策略允许匿名访问，请为广告资助的使用模式生成许可证并将其发送给用户。

在参考实施服务器为使用模型演示发放许可证之前，需要配置服务器以指定为四个使用模型中的每一个模型生成许可证的方式。 这是通过为每个使用模型指定策略来完成的。 “参考实施”包括四个示例策 [!DNL dto-policy.pol]略( [!DNL vod-policy.pol]、 [!DNL sub-policy.pol]、 [!DNL ad-policy.pol])，或者您可以替换您自己的策略。 在中， [!DNL flashaccess-refimpl.properties]设置以下属性以指定用于每个使用模型的策略，并将策略文件放在由属性指定的目录 `config.resourcesDirectory` 中：

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

