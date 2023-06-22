---
description: 我们使用Bento4打包程序和Adobe脱机打包程序来创作加密的DASH内容。 Bento4将输入未加密的mp4内容。
title: 使用Bento4打包您的内容
exl-id: c873eaf6-c738-4f95-a900-a8aecb03754d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 为Widevine和PlayReady打包内容 {#package-for-widevine}

我们使用Bento4打包程序和Adobe脱机打包程序来创作加密的DASH内容。 Bento4将输入未加密的mp4内容。

## 使用Bento4打包您的内容{#package-your-content-with-bento}

Bento4打包器预期输入mp4将预先分段。 Bento4 Packager分发版包含用于此的工具。

**正在调用Bento4**

典型的Bento4打包程序调用如下所示：

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
```

下面的示例结合了PlayReady和Widevine方案。 在此特定情况下，打包程序会将Widevine内容保护和PlayReady内容保护初始化数据添加到输出的DASH内容中。

```
/mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

位置

的值 `--encryption-key` 标记在表单中 `<base16 encoded key id>:<base16 encoded encryption key>`.

此 `--widevine-header=provider:intertrust#content_id:2a` 标记可告知打包程序在清单中包含pssh框，目前TVSDK需要此框才能播放。

的值 `-playready-header` 用于获取PlayReady许可证。

## 使用AdobeOffline Packager打包内容 {#package-your-content-with-adobe-offline-packager}

AdobeOffline Packager将用作输入未加密的mp4内容。

**调用Adobe脱机打包程序**

典型的adobe offline packager调用类似于下面的调用：

```
java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path "Jaigo.mp4"
-out_path "Jaigo_DASH"
-key_file_path "Jaigo_DASH/_info/key.B64.random"
-widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
-widevine_provider intertrust
-playready_LA_URL
http://pr.test.expressplay.com/playready/RightsManager.asmx
-playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
-content_id c595f214d84dc7ecf31a8ebf1b7ddda5
```

在此特定情况下，脱机打包程序会将Widevine内容保护和PlayReady内容保护初始化数据添加到输出DASH内容中。 的值 `-key_file_path` 用于base64编码的键。 的值 `-playready_LA_URL` 用于获取PlayReady许可证。

conf_path参数指向包含以下内容的配置文件：

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

由于某些Android设备(主要是Amazon Fire TV)不支持音频解密，因此音频加密是可选的。
