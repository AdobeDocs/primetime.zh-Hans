---
title: 非SWF应用程序允许列表
description: 非SWF应用程序允许列表
copied-description: true
exl-id: f33fb0e9-144f-49f8-8da2-8a50aea09456
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# 非SWF应用程序允许列表 {#non-swf-application-isting}

AIR是第一个以应用程序允许列表以及用于允许列表非SWF应用程序(Adobe AIR、iOS、Android等)的资产的名称为特征的平台 保留其原始名称： `policy.allowedAIRApplication.n`. 这样，所有在发布之前使用签名证书签名的非Flash应用程序都可以播放内容。 这称为 *应用程序ID*. 您可以使用提取应用程序ID [!DNL AdobePublisherIDUtility.jar] 工具。 此允许列表将在支持Primetime DRM的任何客户端上强制执行。

应用程序ID派生自用于签署特定应用程序的签名证书的公钥。 如果证书中的公钥过期，则所有以前的内容仅允许在用旧证书签名的应用程序上播放，而不会在新应用程序（用新证书签名）上播放。

如果您的情况是，您的内容库允许列出给使用特定签名证书签名的应用程序，并且该证书过期，并且您获得了一个新证书（使用不同的公钥/私钥对），则旧内容不会在新的应用程序上播放 *Unless* 您可以执行以下任一操作：

* 使用 `PolicyUpdateList` ，以覆盖传入的策略，并使用新签名证书的摘要插入新的应用程序允许列表条目。
* 更新许可证服务器的逻辑以覆盖传入策略并插入新的应用程序允许列表条目。
* 请求您的签名证书颁发者向您颁发一个新证书，该证书使用与您的上一个证书相同的公钥/私钥对。
* 如果您要交付引用URL端点的HDS/HLS内容以检索 `DRMMetadata`，您可以重新生成 `DRMMetadata` （使用Primetime DRM Java SDK）插入包含更新的应用程序允许列表条目的新DRM策略。

* 使用具有新签名证书的摘要的新DRM策略重新打包所有旧内容。

参见 `policy.allowedAIRApplication.n` 在 *配置属性* 了解详细信息。

>[!NOTE]
>
>将iOS应用程序添加到允许列表需要您采取一种特殊的方法。 参见 [允许列表iOS应用程序](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) 在 *《 TVSDK for iOS程序员指南》*.
