---
description: 我们使用Bento4包装程序和Adobe脱机包装程序创作加密的DASH内容。 Bento4将作为输入未加密的mp4内容。
seo-description: 我们使用Bento4包装程序和Adobe脱机包装程序创作加密的DASH内容。 Bento4将作为输入未加密的mp4内容。
seo-title: 使用Bento4打包内容
title: 使用Bento4打包内容
uuid: 88323a4e-d0b5-4a41-acec-7126d3e0c90b
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# 打包Widevine和PlayReady的内容 {#package-for-widevine}

我们使用Bento4包装程序和Adobe脱机包装程序创作加密的DASH内容。 Bento4将作为输入未加密的mp4内容。

## 使用Bento4打包内容{#package-your-content-with-bento}

Bento4打包程序希望输入mp4被预分割。 Bento4包装程序分发包含用于此的工具。

**致电Bento4**

典型的Bento4包装程序调用如下所示：

    ./mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —subtitles
    —encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b
    —widevine
    
    -header=2a &quot;CC_300_640x360.mp4&quot;-o &quot;CC_3006_64036&quot;_DASH&quot;
>
    ./mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —subtitles
    —encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
    —playready
    —playready-header=\&quot;LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\&quot;

以下示例结合了PlayReady和Widevine方案。 在这种特殊情况下，包装程序将Widevine内容保护和PlayReady内容保护初始化数据添加到输出DASH内容。

    /mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —subtitles
    —encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b
    —playready
    
    
    
    
    
    —ready-header=&quot;LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\&quot;—widevine-header=provider:intertrust#content_id:2a &quot;CC_300_640x360mp.mp4&quot;-o &quot;CC_300_640x360_DASH&quot;where

标志的值 `--encryption-key` 在表单中 `<base16 encoded key id>:<base16 encoded encryption key>`。

该标 `--widevine-header=provider:intertrust#content_id:2a` 志告知打包程序在清单中包含pssh框，TVSDK当前需要该框才能播放。
此值用于 `-playready-header` 获取PlayReady许可证。

## 使用Adobe Offline Packager打包内容 {#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager将作为输入未加密的mp4内容。

**致电Adobe Offline Packager**

典型的Adobe脱机打包程序调用类似于以下调用：

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml-in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84dcecf31a8ebf1b7ddda5
    -widevine_provider intertrust
    -playready_LA_
    URLhttp://pr.test.expressplay.com/playready/RightsManager.asmx
    
    -playready_keyid c595f284dc7f31aebf7da内容d1b7dddb5-c595f214d84dc7ecf31a8ebf1b7ddda5

在这种特殊情况下，脱机打包程序将Widevine内容保护和PlayReady内容保护初始化数据添加到输出DASH内容。 值为 `-key_file_path` base64编码的键。 其值用于 `-playready_LA_URL` 获取PlayReady许可证。

conf_path参数指向将包含以下内容的配置文件：

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

因为某些Android设备— 主要是Amazon Fire TV — 不支持音频解密，音频加密是可选的。