---
seo-title: 非SWF应用程序白名单
title: 非SWF应用程序白名单
uuid: d4f93b15-e556-4749-95ab-f7f58b1061d7
translation-type: tm+mt
source-git-commit: 9c6a6f0b5ecff78796e37daf9d7bdb9fa686ee0c
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# 非SWF应用程序白名单 {#non-swf-application-whitelisting}

AIR是首个提供应用程序白名单的平台，它是您用于将非SWF应用程序（Adobe AIR、iOS、Android等）白名单化的属性名称。 保留其原名： `policy.allowedAIRApplication.n`. 这允许所有在发布前使用签名证书进行签名的非Flash应用程序播放该内容。 这称为 *应用程序 ID*。 您可以使用该工具提取应用程序 ID [!DNL AdobePublisherIDUtility.jar] 。 此白名单将强制在支持Primetime DRM的任何客户端上。

应用程序 ID源自用于对特定应用程序进行签名的签名证书的公钥。 如果证书中的公钥过期，则仅在使用旧证书签名的应用程序上播放的白名单中列出的所有以前的内容将不在新应用程序（使用新证书签名）上播放。

如果您有一个内容库列在白名单上，并且该内容库已用特定签名证书签名，且该证书已过期且您已颁发新证书（使用不同的公共／私有密钥对），则旧内容将不会在新应用程序上播放，除非您执 *行* 下列任一操作：

* 使用许 `PolicyUpdateList` 可证服务器上的某个条目覆盖传入的策略，并在新签名证书的摘要中插入新的应用程序白名单条目。
* 更新许可证服务器的逻辑以覆盖传入策略并插入新的应用程序白名单条目。
* 请求签名证书颁发者向您颁发一个新证书，该证书使用与您先前的证书相同的公共／私有密钥对。
* 如果您正在传送引用URL端点的HDS/HLS内容以检索该 `DRMMetadata`内容，则可以重新生成 `DRMMetadata` （使用Primetime DRM Java SDK）以插入新的DRM策略，其中包含更新的应用程序白名单条目。

* 使用具有新签名证书摘要的新DRM策略重新打包所有旧内容。

有关详 `policy.allowedAIRApplication.n` 细信 *息，请参阅* “配置属性”。

>[!NOTE]
>
>允许列出iOS应用程序需要一种特殊方法。 请参 [阅《TVSDK for iOS编程](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) 员指南》 *中的“允许列出您的iOS应用程序”*。
