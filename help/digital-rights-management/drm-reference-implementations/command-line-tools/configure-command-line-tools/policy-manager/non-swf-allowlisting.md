---
title: 非SWF应用程序允许列表
description: 非SWF应用程序允许列表
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# 非SWF应用程序允许列表 {#non-swf-application-isting}

AIR是第一个推出应用程序允许列表的平台，以及用于允许列表非SWF应用程序(Adobe AIR、iOS、Android等)的资产的名称 将保留其原始名称： `policy.allowedAIRApplication.n`. 这样，在发布之前使用签名证书签名的所有非Flash应用程序都可以播放内容。 这称为 *应用程序Id*. 您可以使用提取应用程序ID [!DNL AdobePublisherIDUtility.jar] 工具。 此允许列表将在支持Primetime DRM的任何客户端上强制执行。

应用程序ID派生自用于签署特定应用程序的签名证书的公钥。 如果证书中的公钥过期，则所有以前的内容仅允许在用旧证书签名的应用程序上播放，而不会在新应用程序（用新证书签名）上播放。

如果您有一个内容库，该内容库允许列出到使用特定签名证书签名的应用程序，并且该证书到期并且您获得了一个新证书（使用不同的公钥/私钥对），则旧内容将不会在新应用程序上播放 *Unless* 您可以执行以下任一操作：

* 使用 `PolicyUpdateList` 在许可证服务器上覆盖传入的策略，并插入一个新的应用程序允许列表条目以及新签名证书的摘要。
* 更新许可证服务器的逻辑以覆盖传入策略并插入新的应用程序允许列表条目。
* 请求您的签名证书颁发者向您颁发一个新证书，该证书使用与之前证书相同的公钥/私钥对。
* 如果您要交付引用URL端点的HDS/HLS内容以检索 `DRMMetadata`，您可以重新生成 `DRMMetadata` （使用Primetime DRM Java SDK）插入包含更新的应用程序允许列表条目的新DRM策略。

* 使用新的DRM策略重新打包所有旧内容，该策略具有新签名证书的摘要。

请参阅 `policy.allowedAIRApplication.n` 在 *配置属性* 以了解详细信息。

>[!NOTE]
>
>将iOS应用程序添加到允许列表需要您采取特殊方法。 请参阅 [允许列表iOS应用程序](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) 在 *《 TVSDK for iOS程序员指南》*.
