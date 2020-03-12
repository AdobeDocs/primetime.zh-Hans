---
description: 打包内容是准备视频内容以在Web上回放的过程。 打包包括将原始视频转换为清单文件，以及使用不同设备和浏览器的不同DRM解决方案对内容进行选择性加密。
seo-description: 打包内容是准备视频内容以在Web上回放的过程。 打包包括将原始视频转换为清单文件，以及使用不同设备和浏览器的不同DRM解决方案对内容进行选择性加密。
seo-title: 打包内容
title: 打包内容
uuid: b9bc6104-a1ea-4ea0-a0a4-af8a606e5d47
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 打包内容 {#package-your-content}

打包内容是准备视频内容以在Web上回放的过程。 打包包括将原始视频转换为清单文件，以及使用不同设备和浏览器的不同DRM解决方案对内容进行选择性加密。

要准备内容，您可以使用Adobe Offline Packager或其他工具，如ExpressPlay的Bento4 Packager。 打包者既可准备视频以进行回放（例如，将原始文件分割并放入清单中），又可使用您选择的DRM解决方案（PlayReady、Widevine、FairPlay、Access等）保护视频:

* [Adobe Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [ExpressPlay Packager](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. 打包或以其他方式获取用于测试设置的内容。

   打包时要记住的要点之一是，在此打包步骤中使用的密钥ID（内容ID）与您在后续许可令牌请求中必须提供的密钥ID（内容ID）相同。 密钥ID是标识您的CEK(可能存储在您自己的密钥管理数据库中，或使用 [ExpressPlay的密钥存储服务存储)的唯一项](https://www.expressplay.com/developer/key-storage/)。

   >[!NOTE]
   >
   >对于熟悉Adobe Access的用户来说，这是不同解决方案工作方式的重要区别。 在“访问”中，许可证密钥嵌入到DRM元数据中，并随受保护的内容来回传递。 在此处描述的多DRM系统中，实际许可证不会通过，而是会通过密钥ID安全地存储并获取。

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

以下是使用Adobe Offline Packager for Widevine的打包示例。 Packager使用一个配置文件(例如 [!DNL widevine.xml])，它类似于：

```
<config> 
<in_path>sample.mp4</in_path> 
<out_type>dash</out_type> 
<out_path>dash2</out_path> 
<drm/> 
<drm_sys>widevine</drm_sys> 
<frag_dur>4</frag_dur> 
<target_dur>6</target_dur> 
<key_file_path>keyfile.bin</key_file_path> 
<widevine_content_id>2a</widevine_content_id> 
<widevine_provider>intertrust</widevine_provider> 
<widevine_key_id>7debe705d938c76bfd886f077b8fa5f7</widevine_key_id> 
</config>
```

* `in_path` -此入口指向本地打包机上源视频的位置。
* `out_type` -此条目描述打包输出的类型，本例中为DASH（用于HTML5上的Widevine保护）。
* `out_path` -您希望输出转到的本地计算机上的位置。
* `drm_sys` -要打包的DRM解决方案。 这可以是 `widevine`、 `fairplay`或 `playready`。

* `frag_dur` 和是 `target_dur` 特定于DASH的持续时间条目，与视频播放相关。

* `key_file_path` -这是许可证文件在打包机上用作内容加密密钥(CEK)的位置。 它是一个基本64编码的16字节十六进制字符串。
* `widevine_content_id` -这是Widevine的“样板文件”;总是这样 `2a`。 (请勿将此与“”混淆 `widevine_key_id`。)

* `widevine_provider` -出于我们的目的，请始终将其设置为 `intertrust`。

* `widevine_key_id` -这是您在条目中指定的许可证的标 `key_file_path` 识符。 换句话说，它标识您用于加密内容的密钥。 此ID是您自己创建的16字节的HEX字符串。

如 [Packager文档中所述](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf),“作为最佳实践，请创建一个配置文件，其中包含用于生成输出的常用选项。 然后，通过将特定选项作为命令行参数提供来创建输出。” 在这种情况下，我们的配置文件相当完整，因此您可以按如下方式创建输出：

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>命令行参数优先于配置文件参数。 在此示例中，所需的一切都在配置文件中，但我们已使用覆盖了在配置文件中指定的输出路径 `-out_path test_dash/`。

