---
seo-title: 实施使用模型概述
title: 实施使用模型概述
uuid: 1041bb84-9996-4284-b2a0-d6fc6d4b73d9
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# 实施使用模型概述{#implementing-the-usage-models-overview}

参考实施包括业务逻辑，用于演示如何为某个打包内容启用以下四种不同的使用模型：

* 下载自有(DTO)
* 租赁／视频点播(VOD)
* 订阅（可以吃到的）
* 广告资助

要启用使用模型演示，请在打包时指定自定义属性`RI_UsageModelDemo=true`。 如果要使用Media Packager命令行工具打包内容，请指定：

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>如果打包时不激活可选演示模式，则许可证服务器将使用打包时指定的策略颁发许可证。 如果指定了多个策略，则许可证服务器使用第一个有效策略。

在演示中，服务器上的业务逻辑控制所生成许可证的实际属性。 在打包时，内容中只能包含最少的策略信息。 具体而言，策略只需要指示是否需要身份验证才能访问内容。 要启用所有四个使用模型，请包括一个允许匿名访问的策略（对于广告资助的模型）和一个要求用户名／密码身份验证的策略（对于其他3个使用模型）。 当请求许可证时，客户端应用程序可以根据策略中的验证信息确定是否提示用户进行验证。

为了控制用于向特定用户颁发许可证的使用模型，可以将条目添加到参考实施数据库。 `Customer`表包含用于验证用户的用户名和密码。 它还指示用户是否具有订阅。 具有订阅的用户将根据&#x200B;*订阅*&#x200B;使用模式获得许可证。 要在&#x200B;*下载到Own*&#x200B;或&#x200B;*视频点播*&#x200B;使用模型下授予用户访问权，可在`CustomerAuthorization`表中添加一个条目，该条目指定允许用户访问的每段内容和使用模型。 有关填充每个表的详细信息，请参阅[!DNL PopulateSampleDB.sql]脚本。

当用户请求许可证时，引用实施服务器检查客户端发送的元数据以确定内容是否使用`RI_UsageModelDemo`属性进行打包。 如果是，则使用以下业务规则：

* 如果其中一个策略需要身份验证：

   * 如果请求包含有效的身份验证令牌，请在Customer数据库表中查找用户。 如果找到用户：

      * 如果`Customer.IsSubscriber`属性为`true`，则为&#x200B;*订阅*&#x200B;使用模型生成许可证并将其发送给用户。

      * 在`CustomerAuthorization`数据库表中查找此用户和内容ID的记录。 如果找到记录：

         * 如果`CustomerAuthorization.UsageType`是`DTO`，则为&#x200B;*下载到拥有的*&#x200B;使用模型生成许可证，并将其发送给用户。

         * 如果`CustomerAuthorization.UsageType`是`VOD`，则为&#x200B;*视频点播*&#x200B;使用模型生成许可证，并将其发送给用户。
   * 如果所有策略都不允许匿名访问：

      * 如果请求中没有有效的身份验证令牌，则返回“需要身份验证”错误。
      * 否则返回“未授权”错误。


* 如果其中一项策略允许匿名访问，请为广告资助的使用模式生成许可证并将其发送给用户。

在参考实施服务器为使用模型演示颁发许可证之前，需要配置服务器以指定如何为四个使用模型中的每个模型生成许可证。 这是通过为每个使用模型指定策略来完成的。 参考实施包括四个示例策略([!DNL dto-policy.pol]、[!DNL vod-policy.pol]、[!DNL sub-policy.pol]、[!DNL ad-policy.pol])，或者您可以替换您自己的策略。 在[!DNL flashaccess-refimpl.properties]中，设置以下属性以指定用于每个使用模型的策略，并将策略文件放在由`config.resourcesDirectory`属性指定的目录中：

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

