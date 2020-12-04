---
description: 我们使用Bento4包装程序和Adobe脱机包装程序来创作加密的DASH内容。 Bento4将输入未加密的mp4内容。
seo-description: 我们使用Bento4包装程序和Adobe脱机包装程序来创作加密的DASH内容。 Bento4将输入未加密的mp4内容。
seo-title: 使用Bento4打包您的内容
title: 使用Bento4打包您的内容
uuid: 88323a4e-d0b5-4a41-acec-7126d3e0c90b
translation-type: tm+mt
source-git-commit: 75702ea2a524d7b38bb9ac83cb094c8482b1098f
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# 打包Widevine和PlayReady的内容{#package-for-widevine}

我们使用Bento4包装程序和Adobe脱机包装程序来创作加密的DASH内容。 Bento4将输入未加密的mp4内容。

## 使用Bento4{#package-your-content-with-bento}打包您的内容

Bento4包装程序希望输入mp4是预先分段的。 Bento4包装程序分发包含一个用于此的工具。

**正在拔打Bento4**

典型的Bento4包装程序调用如下所示：

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

以下示例结合了PlayReady和Widevine方案。 在此特殊情况下，包装程序将Widevine内容保护和PlayReady内容保护初始化数据添加到输出DASH内容。

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

在哪里

`--encryption-key`标志的值以`<base16 encoded key id>:<base16 encoded encryption key>`的形式显示。

`--widevine-header=provider:intertrust#content_id:2a`标志告诉打包程序在清单中包含pssh框，TVSDK当前要求该框进行播放。

`-playready-header`的值用于PlayReady许可证获取。

## 使用Adobe脱机包装程序{#package-your-content-with-adobe-offline-packager}打包您的内容

Adobe脱机包装程序将作为输入未加密的mp4内容。

**正在调用Adobe脱机包装程序**

典型的adobe脱机包装程序调用类似于以下调用：

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

在这种特殊情况下，脱机打包程序将Widevine内容保护和PlayReady内容保护初始化数据添加到输出DASH内容。 `-key_file_path`的值用于基64编码的密钥。 `-playready_LA_URL`的值用于PlayReady许可证获取。

conf_path参数指向将包含以下内容的配置文件：

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

由于某些Android设备(主要是AmazonFire TV)不支持音频解密，因此音频加密是可选的。
