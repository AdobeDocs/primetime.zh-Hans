---
title: 概述
description: 概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# AIR发布者ID实用程序 {#air-publisher-id-utility}

当您构建AIR文件时，AIR Developer Tool (ADT)会自动生成发布者ID。 AIR发布者ID实用程序( [!DNL AdobePublisherIDUtility.jar])计算AIR应用程序的发布者ID。

发布者ID对于您用于构建AIR文件的证书是唯一的。 如果您为多个AIR应用程序重用同一证书，则所有AIR应用程序都具有相同的发布者ID。 在版本1.5.2之后发行的AIR版本不会将生成的发布者ID添加到文件中。 因此，如果您计划使用AIR应用程序允许列表，请使用此工具确定发布者ID。

>[!NOTE]
>
>用于实施AIR允许列表的发布者ID与应用程序发布者在应用程序的 [!DNL application.xml] 文件。

## AIR发布者ID实用程序命令行用法 {#air-publisher-id-utility-command-line-usage}

```
java -jar AdobePublisherIDUtility.jar 
<i class="+ topic ph hi-d="" i "="">
 <i class="+ topic ph hi-d="" i "="">
  signaturefile 
  java -jar AdobePublisherIDUtility.jar -s 
  <i class="+ topic ph hi-d="" i "="">
    signingcert
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `signaturefile` 指定AIR应用程序的 [!DNL signatures.xml] 文件，位于应用程序 [!DNL META-INF] 目录

* `signingcert` 指定用于签署AIR应用程序的证书

>[!NOTE]
>
>要确定Android应用程序的发布者ID，您需要使用 `-s` 用于指定用于签署Android应用程序包(APK)的证书的选项。 Primetime DRM是构建可以播放受Primetime DRM保护的内容的Android应用程序所必需的。
