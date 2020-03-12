---
description: Adobe Offline Packager将作为输入未加密的mp4内容。
seo-description: Adobe Offline Packager将作为输入未加密的mp4内容。
seo-title: 使用Adobe Offline Packager打包内容
title: 使用Adobe Offline Packager打包内容
uuid: d0676147-c20f-49ea-93a6-9c8dbbbba992
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# 使用Adobe Offline Packager打包内容{#package-your-content-with-adobe-offline-packager}

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
