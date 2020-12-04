---
description: Adobe脱机包装程序将作为输入未加密的mp4内容。
seo-description: Adobe脱机包装程序将作为输入未加密的mp4内容。
seo-title: 使用AdobeOffline Packager打包内容
title: 使用AdobeOffline Packager打包内容
uuid: d0676147-c20f-49ea-93a6-9c8dbbbba992
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# 使用Adobe脱机打包程序{#package-your-content-with-adobe-offline-packager}打包内容

Adobe脱机包装程序将作为输入未加密的mp4内容。

**正在调用Adobe脱机包装程序**

典型的adobe脱机包装程序调用类似于以下调用：

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4
    &quot;-out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random
    &quot;-widevine_key_id c595f214d84dcecf31a8ebf1b7ddda5
    -widevine_intertrust
    -playready_LA_
    
    
    URLhttp://pr.test.expressplay.com/playready/RightsManager.asmx95f214dc7f31a ebf7ddda内容da5eb7ddb7ddda内容idc595f214d84dc7ecf31a8ebf1b7ddda5

在这种特殊情况下，脱机打包程序将Widevine内容保护和PlayReady内容保护初始化数据添加到输出DASH内容。 `-key_file_path`的值用于基64编码的密钥。 `-playready_LA_URL`的值用于PlayReady许可证获取。

conf_path参数指向将包含以下内容的配置文件：

    &lt;config>
    &lt;frag_dur>46&lt;/frag_dur>
    &lt;target_dur>假&lt;/target_dur>
    &lt;encrypt_audio>的&lt;/encrypt_audio>
    &lt;/config>

由于某些Android设备(主要是AmazonFire TV)不支持音频解密，因此音频加密是可选的。
