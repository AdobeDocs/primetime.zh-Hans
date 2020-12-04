---
seo-title: SWF应用程序允许列表
title: SWF应用程序允许列表
uuid: e3021ae9-54f4-4bcf-a274-515ae765f74b
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# SWF应用程序允许列出{#swf-application-allowlisting}

要允许列表SWF应用程序，您可以遵循以下两种策略之一：

* 可以指定SWF的URL。 这是一种非常灵活的方法，尤其是在您定期重建SWF的开发环境中。
* 可以指定SWF哈希。 这是SWF的加密摘要值。 这种方法不那么灵活（但要严格得多），因为SWF HASH在应用程序更改和重新构建时会更改。 在这种情况下，绑定到前一个HASH的所有内容将无法在新播放器上播放，并且必须重新打包。 如果指定[!DNL .swf]文件，[!DNL PolicyManager.jar]工具将自动计算哈希。

   另一方面，如果您通过Flash/Adobe媒体服务器(FMS/AMS)使用Primetime DRM，则可以提供特定SWF的路径，FMS/AMS将自动散列SWF，以便您插入DRM策略，该策略用于打包FMS/AMS流式传输的内容。

有关详细信息，请参阅&#x200B;*配置属性*&#x200B;中的`policy.allowedSWFApplication.n`。
