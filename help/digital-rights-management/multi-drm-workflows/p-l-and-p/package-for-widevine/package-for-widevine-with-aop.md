---
description: AdobeOffline Packager将输入未加密的mp4内容。
title: 使用Adobe脱机打包程序打包您的内容
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 使用Adobe脱机打包程序打包您的内容{#package-your-content-with-adobe-offline-packager}

AdobeOffline Packager将输入未加密的mp4内容。

**正在调用Adobe脱机打包程序**

典型的adobe离线打包程序调用类似于以下调用：

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
    -widevine_provider intertrust
    -playready_LA_URL
    http://pr.test.expressplay.com/playready/RightsManager.asmx
    -playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
    -content_id c595f214d84dc7ecf31a8ebf1b7ddda5

在此特定情况下，脱机打包程序会将Widevine内容保护和PlayReady内容保护初始化数据添加到输出DASH内容中。 的值 `-key_file_path` 用于base64编码的密钥。 的值 `-playready_LA_URL` 用于获取PlayReady许可证。

conf_path参数指向包含以下内容的配置文件：

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

由于某些Android设备(主要是Amazon Fire TV)不支持音频解密，因此音频加密是可选的。
