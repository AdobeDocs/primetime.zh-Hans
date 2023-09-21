---
title: SWF应用程序允许列表
description: SWF应用程序允许列表
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# SWF应用程序允许列表 {#swf-application-allowlisting}

要允许列表SWF应用程序，您可以遵循以下两种策略之一：

* 您可以指定SWF的URL。 这是一种非常灵活的方法，尤其是在您定期重建SWF的开发环境中。
* 您可以指定SWF哈希。 这是SWF的加密摘要值。 这种方法不太灵活（但更为严格），因为SWFHASH将在应用程序更改和重新构建时发生变化。 在这种情况下，绑定到前一个HASH的所有内容将无法在新播放器上播放，并且必须重新打包。 此 [!DNL PolicyManager.jar] 如果您指定 [!DNL .swf] 文件。

  另一方面，如果您通过Flash/Adobe Media Server(FMS/AMS)使用Primetime DRM，则可以为特定SWF提供路径，FMS/AMS会自动散列这些SWF，以便您插入到用于打包由FMS/AMS流式传输的内容的DRM策略中。

请参阅 `policy.allowedSWFApplication.n` 在 *配置属性* 以了解详细信息。
