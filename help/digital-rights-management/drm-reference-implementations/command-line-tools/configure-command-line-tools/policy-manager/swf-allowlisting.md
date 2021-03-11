---
title: SWF应用程序允许列表
description: SWF应用程序允许列表
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# SWF应用程序允许列出{#swf-application-allowlisting}

要允许列表SWF应用程序，可以遵循以下两种策略之一：

* 可以指定SWF的URL。 这是一种非常灵活的方法，尤其是在您定期重建SWF的开发环境中。
* 可以指定SWF哈希。 这是SWF的加密摘要值。 此方法不那么灵活（但要严格得多），因为当应用程序发生更改并重建时，SWF哈希会发生更改。 在这种情况下，绑定到上一个HASH的所有内容都将无法在新播放器上播放，并且必须重新打包。 如果指定[!DNL .swf]文件，[!DNL PolicyManager.jar]工具将自动计算哈希。

   另一方面，如果您通过Flash/Adobe Medium服务器(FMS/AMS)使用Primetime DRM，则可以提供特定SWF的路径，FMS/AMS会自动对SWF进行哈希处理，以便您插入DRM策略，该策略用于打包由FMS/AMS流传输的内容。

有关详细信息，请参阅&#x200B;*配置属性*&#x200B;中的`policy.allowedSWFApplication.n`。
