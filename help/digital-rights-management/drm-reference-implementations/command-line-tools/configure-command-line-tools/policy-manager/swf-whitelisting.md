---
seo-title: SWF应用程序白名单
title: SWF应用程序白名单
uuid: e3021ae9-54f4-4bcf-a274-515ae765f74b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# SWF应用程序白名单{#swf-application-whitelisting}

要将SWF应用程序列入白名单，您可以遵循以下两个策略之一：

* 可以指定SWF的URL。 这是一种非常灵活的方法，尤其是在您定期重建SWF的开发环境中。
* 可以指定SWF哈希。 这是SWF的加密摘要值。 此方法不那么灵活（但要严格得多），因为当应用程序发生更改并重新构建时，SWF HASH会发生更改。 在这种情况下，绑定到上一个HASH的所有内容将无法在新播放器上播放，并且必须重新打包。 如果 [!DNL PolicyManager.jar] 您指定了文件，该工具将自动计算散列 [!DNL .swf] 值。

   另一方面，如果您通过Flash/Adobe Media Server(FMS/AMS)使用Primetime DRM，则可以提供特定SWF的路径，FMS/AMS将自动散列SWF，以便您插入DRM策略，该策略用于打包FMS/AMS流式传输的内容。

有关详 `policy.allowedSWFApplication.n` 细信 *息，请参阅配置* 属性中的。
