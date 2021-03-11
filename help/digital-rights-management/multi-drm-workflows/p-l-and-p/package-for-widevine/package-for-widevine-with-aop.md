---
description: Adobe Offline Packager将作为输入未加密的mp4内容。
title: 使用Adobe Offline Packager打包内容
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# 使用Adobe Offline Packager{#package-your-content-with-adobe-offline-packager}打包您的内容

Adobe Offline Packager将作为输入未加密的mp4内容。

**正在调用Adobe Offline Packager**

典型的adobe脱机打包程序调用类似于以下调用：

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4
    &quot;-out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random
    &quot;-widevine_key_id c595f214d84d7decf31a8ebf1b7ddda5
    -widevine_providertrust
    -playready
    -LA_URLhttp://pr.test.expressplay.com/playready/RightsManager.asmx
    
    -playready_keyid c595f214d84d7f31a ebf8dd1da14d84dc7ecf31a8ebf1b7ddda5

在这种特殊情况下，脱机打包程序会将Widevine内容保护和PlayReady内容保护初始化数据添加到输出DASH内容。 `-key_file_path`的值用于base64编码的键。 `-playready_LA_URL`的值用于PlayReady许可证获取。

conf_path参数指向将包含以下内容的配置文件：

    &lt;config>
    &lt;frag_dur>46&lt;/frag_dur>
    &lt;target_dur>假&lt;/target_dur>
    &lt;encrypt_audio>的&lt;/encrypt_audio>
    &lt;/config>

由于某些Android设备(主要是Amazon Fire TV)不支持音频解密，因此音频加密是可选的。
