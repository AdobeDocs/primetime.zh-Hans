---
seo-title: 非SWF应用程序允许列表
title: 非SWF应用程序允许列表
uuid: d4f93b15-e556-4749-95ab-f7f58b1061d7
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# 非SWF应用程序允许列表 {#non-swf-application-isting}

AIR是首个提供应用程序允许列表的平台，以及您用于允许列表非SWF应用程序（Adobe AIR、iOS、Android等）的属性的名称 保留其原名： `policy.allowedAIRApplication.n`. 这允许所有在发布前使用签名证书进行签名的非Flash应用程序播放该内容。 这称为 *应用程序 ID*。 您可以使用该工具提取应用程序 ID [!DNL AdobePublisherIDUtility.jar] 。 这将允许在支持Primetime DRM的任何客户端上进行列表。

应用程序 ID源自用于对特定应用程序进行签名的签名证书的公钥。 如果证书中的公钥过期，则仅允许列出的所有以前的内容在使用旧证书签名的应用程序上播放，则新应用程序（使用新证书签名）上将不播放。

如果您有一个内容库，它允许列出给使用特定签名证书进行签名的应用程序，并且该证书过期，并且您获得了新证书（使用不同的公共／私有密钥对），则旧内容将不会在新应用程序上播放，除非您执 *行* 下列任一操作：

* 使用许 `PolicyUpdateList` 可证服务器上的某项覆盖传入策略，并在新签名证书的摘要中插入新的应用程序允许列表项。
* 更新许可证服务器的逻辑以覆盖传入策略并插入新的应用程序允许列表项。
* 请求签名证书颁发者向您颁发一个新证书，该证书使用与您先前的证书相同的公共／私有密钥对。
* 如果您正在传送引用URL端点的HDS/HLS内容以检索该 `DRMMetadata`内容，则可以重 `DRMMetadata` 新生成（使用Primetime DRM Java SDK）以插入新的DRM策略，其中包含更新的应用程序允许列表条目。

* 使用具有新签名证书摘要的新DRM策略重新打包所有旧内容。

有关详 `policy.allowedAIRApplication.n` 细信 *息，请参阅* “配置属性”。

>[!NOTE]
>
>允许列出iOS应用程序需要一种特殊方法。 请参 [阅《TVSDK](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) for iOS编 *程师指南》中的*“允许列表您的iOS应用程序”。
