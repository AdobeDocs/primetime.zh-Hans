---
title: 实施使用模型概述
description: 实施使用模型概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# 实施使用模型概述{#implementing-the-usage-models-overview}

参考实施包括业务逻辑，用于演示如何为一个打包内容启用以下四种不同使用模型：

* 下载自带(DTO)
* 租赁/视频点播(VOD)
* 订阅（可以吃的一切）
* 广告资助

要启用使用模型演示，请在打包时指定自定义属性`RI_UsageModelDemo=true`。 如果要使用Media Packager命令行工具打包内容，请指定：

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>如果打包时不激活可选演示模式，则许可证服务器将使用打包时指定的策略颁发许可证。 如果指定了多个策略，则许可证服务器使用第一个有效策略。

在演示中，服务器上的业务逻辑控制生成的许可证的实际属性。 打包时，内容中只能包含最少的策略信息。 具体而言，策略只需要指示访问内容是否需要身份验证。 要启用所有四种使用模式，请包括一种策略，该策略允许匿名访问（对于广告资助的模式），以及一种策略，该策略要求用户名/密码身份验证（对于其他3种使用模式）。 当请求许可证时，客户端应用程序可以根据策略中的验证信息确定是否提示用户进行验证。

为了控制将向特定用户颁发许可证的使用模式，可以将条目添加到参考实施数据库。 `Customer`表包含用于验证用户的用户名和密码。 它还指示用户是否具有订阅。 具有订阅的用户将根据&#x200B;*订阅*&#x200B;使用模式获得许可证。 要在&#x200B;*下载到Own*&#x200B;或&#x200B;*视频点播*&#x200B;使用模型下授予用户访问权，可向`CustomerAuthorization`表添加一个条目，该条目指定允许用户访问的每个内容以及使用模型。 有关填充每个表的详细信息，请参阅[!DNL PopulateSampleDB.sql]脚本。

当用户请求许可证时，Reference Implementation服务器将检查客户端发送的元数据，以确定内容是否使用`RI_UsageModelDemo`属性打包。 如果是，则使用以下业务规则：

* 如果其中一个策略需要身份验证：

   * 如果请求包含有效的身份验证令牌，请在Customer数据库表中查找用户。 如果找到用户：

      * 如果`Customer.IsSubscriber`属性为`true`，则为&#x200B;*订阅*&#x200B;使用模型生成许可证并将其发送给用户。

      * 在`CustomerAuthorization`数据库表中查找此用户和内容ID的记录。 如果找到记录：

         * 如果`CustomerAuthorization.UsageType`为`DTO`，则为&#x200B;*下载到自己的*&#x200B;使用模型生成许可证，并将其发送给用户。

         * 如果`CustomerAuthorization.UsageType`为`VOD`，则为&#x200B;*视频点播*&#x200B;使用模型生成许可证并将其发送给用户。
   * 如果所有策略都不允许匿名访问：

      * 如果请求中没有有效的身份验证令牌，则返回“需要身份验证”错误。
      * 否则，返回“未授权”错误。


* 如果其中一项策略允许匿名访问，请为广告资助的使用模式生成许可证并发送给用户。

在参考实施服务器为使用模式演示颁发许可证之前，需要配置服务器以指定如何为四个使用模式中的每一个生成许可证。 为此，请为每个使用模型指定策略。 “参考实施”包括四个示例策略([!DNL dto-policy.pol]、[!DNL vod-policy.pol]、[!DNL sub-policy.pol]、[!DNL ad-policy.pol])，或者您可以替换您自己的策略。 在[!DNL flashaccess-refimpl.properties]中，设置以下属性以指定用于每个使用模型的策略，并将策略文件放在由`config.resourcesDirectory`属性指定的目录中：

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

