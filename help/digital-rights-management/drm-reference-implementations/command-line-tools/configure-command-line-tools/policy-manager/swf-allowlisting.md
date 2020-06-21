---
seo-title: SWF应用程序允许列表
title: SWF应用程序允许列表
uuid: e3021ae9-54f4-4bcf-a274-515ae765f74b
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# SWF应用程序允许列表{#swf-application-allowlisting}

要允许列出SWF应用程序，您可以遵循以下两种策略之一：

* 可以指定SWF的URL。 这是一种非常灵活的方法，尤其是在您定期重建SWF的开发环境中。
* 可以指定SWF哈希。 这是SWF的加密摘要值。 这种方法不那么灵活（但要严格得多），因为SWF HASH在应用程序更改和重新构建时会更改。 在这种情况下，绑定到前一个HASH的所有内容将无法在新播放器上播放，并且必须重新打包。 如果 [!DNL PolicyManager.jar] 您指定了文件，该工具将自动计算散 [!DNL .swf] 列。

   另一方面，如果您通过Flash/Adobe Media Server(FMS/AMS)使用Primetime DRM，则可以提供特定SWF的路径，FMS/AMS将自动散列SWF，以便您插入DRM策略，该策略用于打包FMS/AMS流式传输的内容。

有关详 `policy.allowedSWFApplication.n` 细信 *息，请参阅* “配置属性”。
