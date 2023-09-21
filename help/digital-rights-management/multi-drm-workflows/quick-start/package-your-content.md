---
description: 打包内容是准备视频内容以供在Web上播放的过程。 打包包括将原始视频转换为清单文件，以及可选地使用针对不同设备和浏览器的不同DRM解决方案对内容进行加密。
title: 打包您的内容
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# 打包您的内容 {#package-your-content}

打包内容是准备视频内容以供在Web上播放的过程。 打包包括将原始视频转换为清单文件，以及可选地使用针对不同设备和浏览器的不同DRM解决方案对内容进行加密。

要准备内容，可以使用AdobeOffline Packager或其他工具，如ExpressPlay的Bento4打包程序。 打包人员既可以准备视频以进行播放（例如，将原始文件分段并将其放入清单），也可以使用您选择的DRM解决方案（PlayReady、Widevine、FairPlay、Access等）保护视频:

* [Adobe脱机打包程序](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [ExpressPlay打包程序](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. 打包或以其他方式获取用于测试设置的内容。

   打包时要记住的关键点之一是，您在此打包步骤中使用的密钥ID（内容ID）与您在后续许可证令牌请求中必须提供的密钥ID相同。 密钥ID是标识CEK的唯一项目（可以存储在您自己的密钥管理数据库中，也可以使用进行存储） [ExpressPlay的密钥存储服务](https://www.expressplay.com/developer/key-storage/).

   >[!NOTE]
   >
   >对于那些熟悉Adobe访问的人来说，这是各种解决方案工作方式的重要差异。 在Access中，许可证密钥嵌入在DRM元数据中，并与受保护的内容来回传递。 在此介绍的多DRM系统中，实际许可证不是传递的，而是安全地存储并通过密钥ID获取。

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

以下是使用AdobeOffline Packager for Widevine的打包示例。 Packager使用配置文件(例如， [!DNL widevine.xml])，它类似于：

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

* `in_path`  — 此入口指向本地打包计算机上源视频的位置。
* `out_type`  — 此条目描述打包输出的类型，在本例中为DASH(用于HTML5上的Widevine保护)。
* `out_path`  — 本地计算机上要输出内容的位置。
* `drm_sys`  — 您打包的DRM解决方案。 这将会是 `widevine`， `fairplay`，或 `playready`.

* `frag_dur` 和 `target_dur` 是特定于短划线的持续时间条目，与视频播放相关。

* `key_file_path`  — 这是用作内容加密密钥(CEK)的打包计算机上的许可证文件的位置。 它是一个Base-64编码的16字节十六进制字符串。
* `widevine_content_id`  — 这是Widevine的“样板”；它始终是 `2a`. (请勿将此问题与 `widevine_key_id`.)

* `widevine_provider`  — 对于我们的目的，请始终将此参数设置为 `intertrust`.

* `widevine_key_id`  — 这是您在 `key_file_path` 进入。 换言之，这标识了您用于加密内容的密钥。 此ID是您自己创建的16字节十六进制字符串。

如附注所述， [Packager文档](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)，“最佳做法是，创建包含要用于生成输出的常用选项的配置文件。 然后，通过提供特定选项作为命令行参数来创建输出。” 在这种情况下，我们的配置文件相当完整，因此您可以按如下方式创建输出：

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>命令行参数优先于配置文件参数。 在此示例中，所需的所有内容均在配置文件中，但我们已使用覆盖配置文件中指定的输出路径 `-out_path test_dash/`.
